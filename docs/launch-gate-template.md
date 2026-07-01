# Launch Gate Template

Use this as a lightweight go / no-go checklist before a production launch.

---

## Launch basics

- **service / launch name:**
- **owner:**
- **launch date / window:**
- **traffic plan:** internal only / canary / partial / full
- **rollback owner:**

## Must-know context

- **what is shipping:**
- **why it matters:**
- **primary user flow affected:**
- **largest failure mode if this breaks:**

## Gate checks

| Gate | Status | Notes |
|---|---|---|
| ownership and on-call are clear | pass / fail / follow-up | |
| dashboards and alerts are ready | pass / fail / follow-up | |
| rollout steps are written down | pass / fail / follow-up | |
| rollback path is known and tested conceptually | pass / fail / follow-up | |
| risky flags / config defaults are reviewed | pass / fail / follow-up | |
| dependency / schema compatibility is understood | pass / fail / follow-up | |
| capacity / traffic assumptions are acceptable | pass / fail / follow-up | |
| success / abort criteria are explicit | pass / fail / follow-up | |

## First 15 minutes plan

- **who is watching dashboards:**
- **who owns rollback if needed:**
- **what metrics decide success:**
- **what signals trigger abort:**

## Known sharp edges

- 
- 
- 

## Decision

- **go / hold / no-go**
- **decider:**
- **time:**
- **notes:**
