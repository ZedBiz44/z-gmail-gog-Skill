# z-gmail-gog Skill Implementation Profile

Date: 2026-09-04 | Prepared by: Skill maintainer | Status: Release candidate, rollout pending

## Identity and Ownership

| Item | Decision |
|---|---|
| Skill display name | z-gmail-gog Skill |
| Skill identifier | `z-gmail-gog` |
| Owner | ZedBiz |
| Repository | `https://github.com/ZedBiz44/z-gmail-gog-Skill` |
| Authoritative branch | `main` unless the authorized human approver approves another branch |
| License and attribution | Original internal ZedBiz work. Link public GOG documentation where technical reference is needed. |
| Classification | Fleet-level internal skill because it will handle private Gmail content, may send external business email, and is intended for later use by multiple agents. |

## Purpose and Scope

| Item | Decision |
|---|---|
| Primary job | Help authorized agents handle Gmail through GOG: read, search, sort, write, reply, draft, send when allowed, follow up, and escalate. |
| Intended users | Authorized ZedBiz AI agents with an outside agent profile and an approved GOG connection to the primary Google account. |
| Test selection | The authorized human approver selects the current test agent or rollout group. Names and current status belong in issue tracking and test records. |
| Included actions | Gmail work described in `SKILL.md` and its references. |
| Excluded actions | GOG install, OAuth authorization, Workspace administration, alias and filter setup, IMAP, Gmail watching, bulk campaigns, automated sequences, and dashboard development. |
| Positive triggers | Business email handling, including support, client advice, confirmations, sales replies, follow-ups, sorting, and Gmail drafts. |
| Do-not-use triggers | Gmail setup or administration, any non-GOG email system, bulk sending, or situations with no active agent profile. |

## Platform and Package

| Item | Decision |
|---|---|
| Supported platform | OpenClaw using GOG for Gmail. |
| Authoring source | This GitHub repository. |
| Deployable package | `dist/z-gmail-gog/`, created from the approved source when the first test is authorized. |
| Required active profile | One outside agent profile per test agent. Finished profiles must not be stored in this repository. |
| Required runtime condition | GOG and OAuth connection to the approved primary Google account must already work. |
| Structural validator | Build the package, then run `python3 /home/ubuntu/z-ai-skill-developer-Skill/scripts/validate_skill.py /path/to/z-gmail-gog-Skill/dist/z-gmail-gog` |
| Platform validation | Fresh OpenClaw session with the selected agent, active outside profile, and documented GOG mode. |

## Controls and Approval

| Item | Decision |
|---|---|
| Default email mode | `draft_only` until the authorized human approver approves send-enabled testing for the individual agent. |
| Human approver | The role named in the active profile approves test results and rollout stages. |
| Technical operator | The implementation operator sets up GOG, OAuth, access controls, profile locations, and skill installation. |
| Wider rollout | Expand only to the group approved for the current rollout after the required tests and records are complete. |
| Stop conditions | Any unexpected sender identity, incorrect profile, GOG failure, private-data issue, unwanted send, blocked action that is bypassed, security concern, or unclear task. |
| Retry limit | Do not repeat a failed action more than twice without diagnosing the failure and getting direction. |

## Security and Rollback

| Item | Decision |
|---|---|
| Security review | [security-and-rollback-review.md](security-and-rollback-review.md) |
| Approved data boundary | Gmail through the approved GOG connection and approved business records only. |
| Approved technical boundary | Use only the GOG actions and OpenClaw permissions provided by the implementation operator. Do not expose credentials. |
| Last known-good commit | Record immediately before the first test. |
| Rollback owner | The authorized human approver makes the operating decision. The implementation operator performs the technical change. |
| Rollback proof | Completed per-agent test or rollback record with the skill state and GOG mode. |

## Completion Proof

| Required proof | Status |
|---|---|
| Repository structural validator passes | Pending |
| Package builds and validates | Pending |
| Every selected profile loads correctly | Pending technical connection |
| Selected rollout test records completed | Pending |
| GOG draft-only block proven | Pending |
| Send-enabled routine email test approved and proven | Pending authorized approval |
| Notion operating SOP created | Pending |
| GitHub issue and journal entry updated | Pending |
| Authorized human approver accepts the next stage | Pending |
