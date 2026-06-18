# Per-field provenance is the core of the governance-model schema

Every `Field` in a `GovernanceModel` carries its own provenance — the `agent` that produced it,
the `citations` it read, a `confidence` score, and a `reviewStatus` — rather than tracking that
metadata separately or only at the model level. We chose this because it lets a *single* data
structure drive four of our five demo beats at once: orchestration visualization (agent +
citations), human-in-the-loop review (flag → approve/edit), self-maintenance (field-level
before/after diffs in the `changelog`), and equal-data-rights comparison (diff the same `FieldKey`
across two entities sharing a `functionId`). The trade-off we accepted is more authoring/emission
cost per field for the engine; the payoff is that the frontend, the review UI, the diff view, and
the comparison view are all just different projections of one frozen contract.

## Consequences

- The engine must emit a `GoldenRun` (`{ events, model }`) per generation; the web app's primary
  demo path replays `events` for an API-failure-proof animation, with a "Live" toggle as the
  brave path. The committed golden runs in `/data` are the on-stage safety net.
- Hypothetical legislation used in the maintenance beat MUST be labeled illustrative — real
  statutes (e.g., Utah Code §81-2-303, §26B-8-125) stay accurate, since the audience is a privacy
  office and judges may know the law.
