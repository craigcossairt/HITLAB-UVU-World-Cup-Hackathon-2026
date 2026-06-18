# Build Plan — overnight sprint (2026-06-17 ~6 PM → 2026-06-18 1:15 PM)

See [CONTEXT.md](../CONTEXT.md) for the locked decisions and domain glossary. This is the execution plan.

## North star
A 5-minute live demo where **Chris B., a privacy officer**, watches AI agents build, review,
and maintain governance models — and surfaces unequal data rights. Story > engineering. Every
hour spent must show up on screen in the pitch.

## Tracks & owners
- **[V] Engine** (Valerie): TypeScript, Anthropic SDK. 10 agent prompts + coordinator. Emits a
  `GoldenRun` (`{events, model}`) per generation (see `shared/governanceModel.ts`). Curates the
  legal corpus. Builds maintenance re-run + diff and the business-license County/City runs.
- **[C] Frontend** (Craig, w/ Claude Code + Claude Design): Next.js + Tailwind + shadcn + React
  Flow + Framer Motion on Vercel. Renders the replay + the model, the review UI, comparison, diff,
  scale grid, SEDI coda. Owns the narration script + judge README.
- **Interface:** the frozen schema. Craig builds against `data/marriage-license/golden-run.sample.json`
  immediately; swap in real engine output at integration.

## Timeline (priority order = your ranking: human-in-loop > orchestration > equal-rights > maintenance > scale)

| Phase | Window | [V] Engine | [C] Frontend | Checkpoint |
| --- | --- | --- | --- | --- |
| 0 · Setup | 6–7 PM | SDK + 1 agent (legal_authority) → real `Field`; stub 10 prompts; coordinator writes `{events,model}` | Scaffold app; load sample golden run; render it raw | Sample renders; one real agent runs |
| 1 · **Core: orchestration + human-in-loop** | 7–11 PM | All 10 agents → all 11 fields for marriage license from corpus; full golden run; validate vs spreadsheet | React Flow agent graph driven by `events`; assembling model panel; **flag → approve/edit → publish v1** | **11 PM: marriage license animates end-to-end w/ human approval. Beats #1+#2 done.** |
| 2 · Equal data rights | 11 PM–1:30 AM | Business license for **County** + **Municipality** (same `functionId`, divergent class/retention) → 2 runs | Side-by-side compare; diff shared `fieldKey`s; inequality flag + harmonization banner | 1:30 AM: equal-rights beat done (#3) |
| 3 · Maintenance (lighter/canned) | 1:30–3:30 AM | Monitor agent + re-run affected fields on a **labeled hypothetical bill** → v2 + changelog diff | Version timeline + before/after diff view; approve → v2 | 3:30 AM: maintenance beat done (#4) |
| 4 · Scale (lighter/static) | 3:30–5 AM | Fast live business-license run for the on-stage Live toggle (+ cached fallback) | Entity × function grid (`ScaleGridCell[]`); hero published, business live, rest "ready" | 5 AM: full spine complete (#5) |
| 5 · SEDI coda + arch diagram | 5–6:30 AM | — (support) | Policy ↔ SEDI/KERI ↔ healthcare layer; **SSN before/after overlay** | SEDI bonus in |
| 6 · Integration + deploy | 6:30–9 AM | Hand over real golden runs; commit to `/data` | Swap sample→real; deploy to Vercel; verify on demo laptop + network | Live URL works |
| 7 · **FREEZE** → polish + rehearse | 9 AM–12 PM | freeze | Visual polish (Claude Design); rehearse 5-min demo 3×; judge-Q&A prep; judge README + arch diagram | Demo timed ≤5 min |
| 8 · Buffer + depart | 12–1:15 PM | — | Final deploy check; **save a screen recording of a perfect run**; backup local copy | Leave 1:15 PM |

If behind at the 11 PM checkpoint: protect the core. Cut maintenance depth first, then make scale
fully static. Never cut human-in-loop or orchestration.

## Curated corpus to pre-load (`data/corpus/`) — [V]
- **Marriage:** Utah Code §81-2-303 (incl. (4) SSN), §26B-8-125 (vital records classification),
  §63G-2-302 (GRAMA private), Vital Records **GRS-285** (retention).
- **Business license:** county licensing (Utah Code Title 17) + municipal licensing (Title 10/11 +
  a sample local ordinance); GRAMA §63G-2 classification; applicable business-license GRS. *(Pin
  exact cites; approximate-but-clearly-labeled is acceptable for the demo.)*
- **Maintenance trigger:** a **clearly-labeled hypothetical** Utah bill (e.g., "H.B. — illustrative:
  restricts SSN retention on vital-record applications"). **Never present fabricated law as real.**

## Demo-safety net (non-negotiable)
1. Golden runs committed to `/data`; the **replay path is the default** — no live API call needed to demo.
2. The "Live" toggle is used only for the business-license live-gen moment, with the cached run one key away.
3. App runs **fully offline** from static JSON.
4. A **screen recording** of one perfect 5-min run saved locally as the ultimate fallback.

## Open items needing a human decision (quick)
- Entity names to feature: **Utah County** (unincorporated) vs **Orem City** — same county region, divergent governance.
- Exact text of the hypothetical maintenance bill (Valerie to draft, labeled illustrative).
- Anthropic API key + Vercel project (set up in Phase 0).
