# ITD110 Consolidation — Design

Date: 2026-11-25 · Status: approved · Template: `MirkoLouis/ITE183`

## Intent
Make ITD110 one repo with one folder per activity, like ITE183/ITD105.
`ITD110-Act2` already holds act2–act4 and Case Study 2 but has broken
gitlinks (`act1` → itd110@c95f702, `Case Study 1 - Pounce` →
Pounce@eaeb467, no `.gitmodules`), committed Redis dumps, and a stale
duplicate repo (`ITD110-Act3`).

## Goals
- `act1/` holds itd110's full history, rewritten into the folder.
- Broken `Case Study 1 - Pounce` gitlink removed; README links to Pounce.
- `dump.rdb` and `act2/dump.rdb` untracked and ignored.
- README index of all activities.
- Final names: `ITD110-Act2` → `ITD110`; `itd110` → `ITD110-Act1` (archived);
  `ITD110-Act3` archived. Both archived repos carry a "Moved" note.

## Non-goals
- Pounce stays a standalone, active portfolio repo.
- BidBlitz and Lister-Sorter are not ITD110 work.
- Renaming `master` → `main`.
- Purging `dump.rdb` from history (would need a force push).
- The user's uncommitted local edits in `~/Documents/ITD110` stay local.

## Approaches
| Approach | Trade-off | Decision |
|---|---|---|
| Fix ITD110-Act2 in place, then rename | Keeps 21 commits and SHAs; no force push; PR-able | **Chosen** |
| Fresh repo like ITE183 | Changes all Act2 SHAs; same rename needed for the name | Rejected |

GitHub names are case-insensitive: `ITD110` collides with `itd110`, so
`itd110` is renamed to `ITD110-Act1` before `ITD110-Act2` → `ITD110`.

## Process decisions
- Act2 changes: branch `chore/consolidate-itd110` → PR into `master`; the user merges.
- "Moved" notes on itd110/ITD110-Act3 go directly to their `main` (user approved).
- Order after merge: notes → rename itd110 → archive both → rename ITD110-Act2.
