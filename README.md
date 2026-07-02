# predictpaul-track

Public, verifiable **paper-trading** track record for [PredictPaul](https://github.com/mobius0087x), a Polymarket whale-following signal verifier. A daily job exports the exact JSON responses of PredictPaul's local read-only API into this repository and commits them.

## Why a Git repo?

**The commit history is the timestamp audit trail.** Every snapshot is committed on the day it was produced; GitHub records the push time independently of us. Signals and positions are committed *before* their markets resolve, so outcomes cannot be cherry-picked or backfilled after the fact. Anyone can:

1. `git log -p positions.json` — watch positions appear ex-ante and settle later.
2. Verify the hash chain in `positions.json`: each entry's `hash` is the SHA-256 of its sealed fields (`seq, market_id, direction, entry_price, p_model_side, size_frac, stake, bankroll_before, prev_hash`), and each `prev_hash` must equal the prior entry's `hash`. Rewriting history breaks the chain — and would also show up as a force-push anomaly in commit timestamps.

## Files

| File | Contents |
|------|----------|
| `track-record.json` | Summary of the paper ledger: bankroll, total return, hit rate, equity curve, tamper check. |
| `signals.json` | All recorded forward signals (open + settled) with entry prices, edges, whale stats, plus a rolling report. |
| `positions.json` | The full hash-chained paper ledger (every position, sealed at open) + `chain_ok` verification result. |
| `forward-report.json` | Rolling after-cost EV summary over the forward log (hit rate, mean/median/cumulative PnL). |
| `meta.json` | `generated_at` timestamp of the last export. |

The JSON structures are byte-for-byte identical to the local PredictPaul API endpoints (`/track-record`, `/signals`, `/positions`, `/forward-report`) — this repo is a drop-in mirror.

## Disclaimer

**PAPER TRADING ONLY — edge unproven.** No real money is at stake. These numbers are a forward experiment in progress, not investment advice and not evidence of a profitable strategy. Sample sizes are small; treat everything here as "accumulating evidence", not results.
