# Release Review Template

Use this for:

- risky deploys
- migrations
- configuration changes
- dependency upgrades with production impact
- rollout reviews before a launch window

---

## Change summary

- **service / repo:**
- **owner:**
- **review date:**
- **target environment:**
- **planned rollout window:**
- **change type:** code / config / schema / infra / traffic / other

## What is changing

Briefly describe:

- what is changing
- why now
- what user or system behavior should improve

## Risk summary

| Risk | Severity | Why it matters | Mitigation / rollback |
|---|---|---|---|
| example: migration lock contention | high | can block writes | rollout off-peak, abort on latency spike |

## Scope and blast radius

- **critical user flow(s) touched:**
- **dependencies touched:**
- **canary / partial rollout available?**
- **expected blast radius if this goes bad:**
- **regions / tenants / environments affected:**

## Pre-release checks

- [ ] service owner reviewed change scope
- [ ] rollout plan is written down
- [ ] rollback owner is explicit
- [ ] rollback command / action is known
- [ ] dashboards and logs for first-check validation are listed
- [ ] alert expectations are known
- [ ] timeout / retry / config risk is understood
- [ ] schema / cache / queue compatibility is reviewed

## Observability to watch

- **dashboard links:**
- **key metrics:** error rate / latency / saturation / queue depth / throughput
- **log queries to keep open:**
- **alerts expected during rollout:**
- **success signals within first 5–15 minutes:**

## Rollout plan

1. 
2. 
3. 

## Abort / rollback criteria

- abort if:
  - 
  - 
- rollback action:
  - 
- rollback owner:
  - 

## Data and compatibility notes

- [ ] backward compatibility reviewed
- [ ] forward compatibility reviewed
- [ ] migration order documented
- [ ] replay / reconciliation plan exists if needed
- [ ] duplicate processing / idempotency risk reviewed

## Open follow-ups before release

- [ ] 
- [ ] 
- [ ] 

## Final release decision

- **status:** go / go with follow-ups / no-go
- **decision owner:**
- **notes:**
