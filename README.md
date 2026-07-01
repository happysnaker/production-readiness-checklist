# production-readiness-checklist

A practical production readiness checklist for backend services, release reviews, launch gates, and on-call handoffs.

This repository is meant to be a **copy-pasteable, implementation-minded checklist** for engineers shipping real services — not a vague essay about "best practices".

Use it before:
- first production launch
- major architecture changes
- high-risk releases
- service ownership handoffs
- on-call rotations
- design / go-live reviews

## Who this is for

- backend engineers
- Go / Java service owners
- tech leads and reviewers
- SRE / platform engineers
- teams preparing a release or production launch

## How to use it

1. Copy the sections relevant to your service into your release doc, PR template, or launch checklist.
2. Mark each item as **done / not applicable / follow-up required**.
3. Treat unchecked items as explicit risk, not invisible debt.
4. Re-run the checklist after major infra, data, or traffic changes.

---

## 1) Ownership, scope, and blast radius

- [ ] Service owner / team is clearly defined.
- [ ] Primary on-call or escalation path is documented.
- [ ] Service purpose, critical user flows, and dependencies are documented.
- [ ] Blast radius is understood if the service is degraded or unavailable.
- [ ] Rollout scope (all traffic / canary / internal only / region-by-region) is explicit.
- [ ] Rollback owner and rollback trigger are defined.

## 2) Runtime configuration and secrets

- [ ] All required config keys are documented.
- [ ] Production defaults are explicit; nothing relies on local-dev assumptions.
- [ ] Secrets are injected from a proper secret manager or deployment system.
- [ ] No secrets, tokens, or private keys are committed to the repo.
- [ ] Config validation fails fast on startup when required values are missing.
- [ ] Risky feature flags have safe defaults.
- [ ] Environment-specific behavior is intentional and documented.

## 3) Startup, shutdown, and health

- [ ] Readiness probe reflects actual dependency readiness.
- [ ] Liveness probe does not flap on normal transient dependency issues.
- [ ] Graceful shutdown is implemented and tested conceptually.
- [ ] In-flight requests / jobs are handled safely during shutdown.
- [ ] The service can start with dependencies temporarily unavailable when appropriate.
- [ ] Crash-loop behavior and startup timeout expectations are understood.

## 4) Logging, metrics, tracing, and debugging

- [ ] Structured logs include request / trace / correlation identifiers where relevant.
- [ ] Log level policy is defined for production.
- [ ] Sensitive fields are redacted from logs.
- [ ] Core RED / USE metrics exist where relevant.
- [ ] Error rate, latency, throughput, saturation, and queue/backlog signals are covered.
- [ ] Metrics and dashboards distinguish success, failure, timeout, and cancellation paths.
- [ ] Tracing is enabled for the critical request path where practical.
- [ ] There is a fast way to answer: "is it broken, slow, or overloaded?"

## 5) API behavior and failure handling

- [ ] Timeouts are set deliberately for inbound and outbound calls.
- [ ] Retry policy is explicit and avoids retry storms.
- [ ] Idempotency expectations are documented for write operations.
- [ ] Dependency failures degrade gracefully where possible.
- [ ] Error responses are actionable and consistent.
- [ ] Backpressure / rate limiting behavior is defined.
- [ ] Partial failure behavior is documented for fan-out / async workflows.
- [ ] High-cardinality user input does not explode labels / logs / cache keys.

## 6) Data correctness and storage

- [ ] Schema / migration plan is documented.
- [ ] Backward / forward compatibility is considered for deploy order.
- [ ] Rollback plan for schema changes is explicit.
- [ ] Data retention / TTL policy is defined where relevant.
- [ ] Critical writes are durable enough for the product requirement.
- [ ] Reconciliation / replay strategy exists for async pipelines.
- [ ] Duplicate event / duplicate request handling is defined.
- [ ] Capacity limits for DB / cache / queue are known.

## 7) Security and access control

- [ ] AuthN / AuthZ boundaries are documented.
- [ ] Least-privilege credentials are used for dependencies.
- [ ] Internal admin / debug endpoints are protected.
- [ ] Security-sensitive events are auditable.
- [ ] Input validation exists on untrusted boundaries.
- [ ] Dependency and container image update posture is understood.
- [ ] Publicly exposed routes, ports, and ingress rules are reviewed.
- [ ] Secrets rotation path is known.

## 8) Deployments, rollback, and release safety

- [ ] Deployment strategy is defined (rolling / canary / blue-green / batch).
- [ ] Rollback can be executed without improvisation.
- [ ] Deploy and rollback commands / runbook are documented.
- [ ] Release health signals are identified before rollout starts.
- [ ] Success / abort criteria are explicit.
- [ ] A bad deploy can be detected within minutes, not hours.
- [ ] Dependency version / config drift risk is understood.
- [ ] The team knows which changes require extra caution (migrations, cache key changes, traffic shifts, auth changes).

## 9) Performance, load, and capacity

- [ ] Expected traffic shape is documented.
- [ ] Known bottlenecks are identified.
- [ ] Capacity assumptions are written down.
- [ ] Expensive code paths, queries, or fan-outs are visible in metrics/traces.
- [ ] Resource limits / requests are reasonable.
- [ ] Concurrency controls and worker pool limits are intentional.
- [ ] Cache strategy is documented if latency depends on it.
- [ ] There is a plan for sudden traffic spikes or dependency slowdown.

## 10) On-call readiness and incident response

- [ ] Alerts exist for symptoms that matter.
- [ ] Alerts are actionable and not pure noise.
- [ ] Runbooks exist for top failure modes.
- [ ] Dashboards linked from alerts are useful.
- [ ] The team knows how to disable risky paths / feature flags in an incident.
- [ ] Escalation contacts and ownership boundaries are clear.
- [ ] Known failure modes and recent incidents are documented.
- [ ] Manual recovery steps are written down.

## 11) Cost and operational hygiene

- [ ] Cost drivers are understood (storage, egress, CPU, queue volume, third-party calls).
- [ ] Log / metric / trace cardinality is kept under control.
- [ ] Expensive background jobs are visible and rate-limited.
- [ ] Orphaned resources / stale data cleanup is covered.
- [ ] SLO / reliability decisions are aligned with actual product value.

## 12) Final go-live questions

Before shipping, can the team answer **yes** to these?

- [ ] If this deploy goes bad, we know how to detect it fast.
- [ ] If this deploy goes bad, we know how to stop or roll it back fast.
- [ ] If latency spikes, we know which dashboards and logs to open first.
- [ ] If a dependency fails, we know the user-visible impact.
- [ ] If an alert fires at 3am, the on-call engineer has enough context to act.
- [ ] If traffic doubles, the most likely bottleneck is already known.

---

## Common failure patterns this checklist is trying to catch

- health checks that lie
- retries that multiply incidents
- migrations with no rollback path
- dashboards that look pretty but answer nothing
- missing runbooks for obvious failure modes
- secrets/config drift between environments
- shipping without clear abort criteria
- launching a service nobody truly owns

## Related repos

- [backend-engineer-checklist](https://github.com/happysnaker/backend-engineer-checklist) — broader backend engineering roadmap / study checklist
- [system-design-checklist](https://github.com/happysnaker/system-design-checklist) — architecture and design-review oriented checklist
- [go-service-starter](https://github.com/happysnaker/go-service-starter) — minimal production-minded Go HTTP service starter
- [go-http-middleware-kit](https://github.com/happysnaker/go-http-middleware-kit) — reusable `net/http` middleware for operational basics

## Contributing

Suggestions are welcome, especially if they come from real launch reviews, incident retrospectives, or production hardening work.

If you have a checklist item that has repeatedly prevented incidents on your team, open an issue or PR.

## Support

If this checklist saved your team time during a launch review or release prep, you can support ongoing maintenance here:

- [Support page](https://happysnaker.github.io/support/)

Typical support fit:

- **¥9.9** — if one section caught a release risk
- **¥19.9** — if it helped a real launch review or handoff
- **¥99** — if you want lightweight async feedback on a release checklist, public repo README, or technical profile packaging
