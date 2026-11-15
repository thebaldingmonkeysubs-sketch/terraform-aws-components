# Multi-Agent Terraform Governance POC — source repository guide

> **This is the experiment-specific README for this fork.** The existing root [README.md](./README.md) is Cloud Posse's generated upstream project documentation and should be preserved. This POC guide describes additional repository ownership, agent onboarding and governance requirements; it does not modify upstream Terraform code.

**Repository:** `thebaldingmonkeysubs-sketch/terraform-aws-components` (public fork of `cloudposse/terraform-aws-components`). The original component monorepo is archived after components migrated into separate Cloud Posse repositories. For this experiment the fork provides a **stable, realistic Terraform source baseline**. Pin the exact commit SHA of `main` when starting a test run.

## What this repository does

Contains the **Terraform code** to be examined by the Phase 1 experts and modified by authorised coding agents during subsequent POC phases. It is **not** the home of the master prompts, specialist KBs, the authoritative audit/compliance policy, or the test evidence archive.

Its `modules/` tree holds AWS components with code, interfaces and documentation; **module presence alone does not establish that they are directly connected**. Researchers must distinguish existing code dependencies from deliberately designed future sandbox integrations.

## Initial ten specialist-owned module scopes

| Specialist | Owned module path | Primary expertise |
|---|---|---|
| `iam-role-expert` | `modules/iam-role/` | Role and policy contracts, least privilege |
| `s3-bucket-expert` | `modules/s3-bucket/` | S3 configuration, bucket policy, encryption |
| `kms-expert` | `modules/kms/` | Key management, grants and encryption |
| `cloudtrail-expert` | `modules/cloudtrail/` | Audit trail configuration and outputs |
| `cloudtrail-bucket-expert` | `modules/cloudtrail-bucket/` | Secure audit-log storage |
| `cloudwatch-logs-expert` | `modules/cloudwatch-logs/` | Log groups, retention and monitoring |
| `vpc-expert` | `modules/vpc/` | Networking and flow-log integration |
| `vpc-flow-logs-bucket-expert` | `modules/vpc-flow-logs-bucket/` | Network log storage and retention |
| `aws-config-expert` | `modules/aws-config/` | Configuration inventory/compliance |
| `security-hub-expert` | `modules/security-hub/` | Security findings and integrations |

**Ownership scope is a proposed engineering policy, not yet a GitHub permission.** Each expert researches its module in Phase 1. In Phase 2+ code changes require valid server-side reservations and required governance checks. A specialist wanting a different owner's code changed must initiate a recorded handoff or intent negotiation with the owner; it may not directly edit that owner's protected integration scope.

## Where everything else lives

| Repository | Purpose |
|---|---|
| [MassiveAIAgentGroundWork](https://github.com/thebaldingmonkeysubs-sketch/MassiveAIAgentGroundWork) | Phase runbooks, Claude Code prompts and planned coordination/governance design |
| [MassiveAIAgentKnowledge](https://github.com/thebaldingmonkeysubs-sketch/MassiveAIAgentKnowledge) (private) | **All-agent cross-project knowledge repository** (coding, orchestration, governance, compliance research, reviewers and future domains); the ten Terraform expert KBs and Phase 1 reports are its first workload |
| [MassiveAIAgentAuditCompliance](https://github.com/thebaldingmonkeysubs-sketch/MassiveAIAgentAuditCompliance) (private) | Approved policy baselines, audit-steward proposals, policy tests and approval decisions |
| [MassiveAIAgentTestCodeRepo](https://github.com/thebaldingmonkeysubs-sketch/MassiveAIAgentTestCodeRepo) (private) | Isolated fixtures, simulated conflict scenarios, malicious/no-reservation tests and results |
| **terraform-aws-components** (this repo) | Actual Terraform source and module contracts for the experiment |

The [Phase 1 runbook](https://github.com/thebaldingmonkeysubs-sketch/MassiveAIAgentGroundWork/blob/poc/phase-1-agent-preparation/docs/PHASE_1_RUNBOOK.md) and [single consolidated Claude Code prompt pack](https://github.com/thebaldingmonkeysubs-sketch/MassiveAIAgentGroundWork/blob/poc/phase-1-agent-preparation/docs/PHASE_1_CLAUDE_CODE_PROMPTS.md) are on the GroundWork preparation branch pending review.

## Lifecycle

**Phase 0 — independent enforcement infrastructure:** configure trusted reservation and interruption service, MCP interface, protected policy repository, GitHub App / required checks, and test gates. Merely adding `AGENTS.md`, a persona or this README cannot enforce anything.

**Phase 1 — research-only:** ten module specialists analyse source and write their own KB/persona files **in MassiveAIAgentKnowledge**, while a separate audit policy steward proposes controls for independent approval. The source fork is read-only; pin the source SHA, cite precise file/symbol evidence, and publish two Phase 1 reports in Knowledge. Do not change Terraform here.

**Phase 2 — Claude Code swarm:** main coordinator reads approved rules and KB snapshots, assigns GitHub Issues, and allows edits only under authorised reservations. Other owners accept/reject cross-module handoffs. The trusted gate revalidates current status at integration.

**Phase 3 — mixed Claude Code + Codex:** Codex agents initially behave like new contributors. Unauthorised PRs receive deterministic failed checks with actionable instructions (reserve intent, conduct impact analysis, obtain necessary handoffs, rerun validations). Agents may revise their work and reapply under the same rules.

**Phase 4 — rogue agents:** intentionally ignore prompts or attempt a branch/status/permission bypass. The preventive gate must stop unauthorised merges **even when the agent does not cooperate**.

## Non-negotiable experimental rules

- No coding agent receives credentials that can override protected branch rules, governance checks, approved compliance controls, or live infrastructure.
- No agent (including the audit steward) can self-approve a policy relaxation or make its own PR check authoritative.
- A reservation alone is not an approval; approved intent, current policy version, changed paths, interruptions, integration tests and integration-authorisation state must be considered.
- GitHub Issues and handoff discussions provide a durable narrative; the **external coordination service** holds the authoritative reservation/interrupt state. GitHub/MCP services must be actually deployed and verified before claiming preventive enforcement.
- Compliance scanner findings use `PASS`, `FAIL` or `UNDETERMINED`, with revision/evidence, and deduplicate issue creation. **A continuous scanner is planned, not activated by this README.**
- Start with offline/static Terraform validation; **do not run `terraform apply` or deploy actual AWS resources** during the initial POC.
- Do not edit Cloud Posse's generated upstream README by hand; place POC-specific changes in this file.

## First step

Review GroundWork Phase 1 PR and start a fresh Claude Code session with the consolidated Phase 1 **Prompt A**, after verifying the four related checkouts and explicitly recording any missing enforcement machinery as `NOT ENFORCED`. Specialist KBs, authoritative compliance policies, and runbooks must remain separately owned.
