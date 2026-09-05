# Agent Profile and Permissions

The shared skill does not contain a roster of agents, personal email addresses, server names, passwords, tokens, or temporary test details. Each finished agent profile lives outside this package and is managed by the implementation operator.

Before using Gmail, load the profile provided for the active agent. Check that the profile shows the right agent name, role, sender address, owner label, email mode, approval contact, and business-record location. Stop if any of those details are missing or do not fit the current task.

## Profile Fields

| Field | What it tells the agent |
|---|---|
| `agent_name` | The agent using the profile. |
| `role` | The email work that normally fits the agent’s job. |
| `primary_google_account` | The approved Google account connected through GOG. |
| `from_name` | The display name shown to email recipients. |
| `from_email` | The exact approved sender address for new email and normal replies. |
| `reply_to` | The approved address where replies should go. |
| `owner_label` | The `Agent/{AgentName}` Gmail label that belongs to this agent. |
| `email_skill_enabled` | Whether the agent should use this skill. This is guidance unless the technical setup enforces it. |
| `email_mode` | Either `draft_only` or `send_allowed`. |
| `may_send_routine_email` | Whether routine email may be sent. This remains subject to the real GOG permission. |
| `automatic_email_handling` | Whether a separate email automation may start work automatically. The generic skill does not create that automation. |
| `normal_email_types` | The kinds of email the agent normally handles. |
| `writing_tone` | The style the agent should use when writing. |
| `approval_contact_role` | The person or role who makes sensitive decisions. |
| `must_ask_approver_for` | Situations that always require human approval. |
| `business_record_location` | Where important business notes belong, or `NONE`. |
| `may_update_business_records` | Whether the agent may update the approved business record. |

## Permission Meanings

The profile tells an agent what it should do. It does not create a hard technical boundary by itself. The implementation operator must enforce permissions through the GOG installation, account access, and server controls.

| Profile setting | Agent instruction | Required technical control |
|---|---|---|
| `email_skill_enabled: false` | Do not use Gmail through this skill. | The email tool or agent access must deny Gmail actions. |
| `email_mode: draft_only` | Read, sort, and create drafts only. | GOG must block send commands. |
| `email_mode: send_allowed` | Send routine email within the assigned role. | GOG must permit sending, while the skill continues to require approval for risky matters. |
| `from_email` | Use only this sender identity. | A future controlled email tool can force this value. GOG safety profiles cannot hard-lock a text sender address. |
| `owner_label` | Work from this label and leave other ownership labels alone. | Gmail labels organize the account. A controlled email tool is needed if label boundaries must be technically enforced. |

## Correct Sender Address

For new email, pass the profile’s exact sender address to GOG and confirm it is an approved Gmail send-as address. For replies, use the profile’s exact sender address. GOG may choose the verified alias that received the message when its addressed-alias option is used, but stop if that address differs from the profile.

A GOG send command must use a verified send-as address. A profile or skill does not make an alias available. Alias creation and Gmail send-as setup are separate technical work.

## Profile Loading Check

Before working on email, state internally:

```text
Active agent: [agent_name]
Approved sender: [from_email]
Owner label: [owner_label]
Email mode: [email_mode]
Human approver: [approval_contact_role]
```

If the assignment needs a different identity, label, or permission, stop instead of changing the profile yourself.

## Example Profile

See [example-agent-profile.yaml](../templates/example-agent-profile.yaml). It uses placeholders only and is not an active configuration file.

## Technical References

GOG supports an explicit `--from` address for replies. The address must be a verified send-as alias. See the [GOG reply command reference](https://github.com/openclaw/gogcli/blob/main/docs/commands/gog-gmail-reply.md).

GOG safety profiles can block commands, including send commands, before Google is called. They cannot hard-lock arbitrary text values such as one particular sender address. See the [GOG safety-profile reference](https://github.com/openclaw/gogcli/blob/main/docs/safety-profiles.md).
