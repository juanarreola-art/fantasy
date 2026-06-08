---
name: pick-fantasy-xi
description: Choose a valid daily Fantasy XI from the official tournament game board.
---

Use this skill when selecting the daily Fantasy XI.

Primary objective:
Return exactly 11 eligible player IDs from the current daily game board, using a valid formation and a balanced point-maximizing strategy.

Required formation:

- Exactly 1 GK.
- 3 to 5 DEF.
- 3 to 5 MID.
- 1 to 3 FWD.
- Exactly 11 total players.

Source-of-truth rules:

1. Read `prompt.md`, `rules/`, `output-format/`, and the files in `game-board/` before choosing.
2. Use `game-board/players.json` as the source of truth for daily player eligibility.
3. Use only player IDs present in the daily board.
4. Do not select a player who is not eligible for the current matchday.
5. Do not invent IDs, positions, teams, statistics, or fixture data.
6. Treat missing, unavailable, null, or ambiguous metadata as a small uncertainty penalty rather than proof that a player is poor.
7. Base the lineup on the provided tournament files. Do not rely on external systems, private data, or unavailable context.

Selection process:

1. Build eligible pools by position: GK, DEF, MID, FWD.
2. Remove or downgrade players when the board clearly indicates they are ineligible, suspended, unavailable, injured, unlikely to play, or outside the current fixtures.
3. Estimate each player's fantasy value with the ranking rules below.
4. Choose the best valid formation from available candidates, with a preference for attacking formations when the evidence supports them.
5. Prefer the lineup with the strongest expected points while preserving formation validity.
6. Before final output, re-count positions and verify that all 11 IDs are unique and eligible.

Player ranking rules:

1. Minutes are the highest priority. Prefer players likely to start and likely to play 60 or more minutes.
2. Use a balanced player profile: reliable starters are preferred, but FWD and attacking MID candidates receive an upside premium when their minutes outlook is credible.
3. For all positions, prior starts and prior appearances are useful positive signals when current data is limited.
4. For FWD and attacking MID, prioritize goal involvement: goals, assists, shots, attacking role, set pieces, and strong team scoring context when available.
5. For DEF and GK, prioritize clean-sheet chance, team defensive strength, and favorable matchup context when available.
6. For GK, also value likely save volume, but do not prefer a heavily pressured goalkeeper over a strong clean-sheet candidate unless the board strongly supports it.
7. Avoid players with high card risk when similar alternatives exist, especially defenders and defensive midfielders.
8. Prefer balanced certainty over celebrity value. A famous player with weak minutes evidence is not automatically better than a reliable starter.
9. If the board includes current tournament or selected-day stats, prefer those over older historical stats.
10. If only prior World Cup stats are available, use them as weak supporting signals, not decisive proof.
11. If venue, host status, or home advantage appears in the board, use it only as a small tie-breaker. Do not override stronger evidence from minutes, role, matchup quality, or current stats.
12. Do not apply a special preference for any one country unless the official board data supports that choice.

Formation guidance:

1. Prefer 1 GK, 3 DEF, 4 MID, 3 FWD when there are enough strong, likely-starting forwards.
2. Use 1 GK, 4 DEF, 4 MID, 2 FWD when the player pool is balanced or forward minutes are uncertain.
3. Use 1 GK, 5 DEF, 3 MID, 2 FWD only when clean-sheet opportunities are clearly stronger than attacking options.
4. Never force a preferred formation if another valid formation has safer starters and stronger expected points.

Contrarian guidance:

1. Do not choose weaker players only to be different.
2. When two or more candidates are close in expected value, prefer the less obvious differentiated pick if it remains well supported by eligibility, minutes, and matchup evidence.
3. Limit differentiation to tie-breakers. Expected points and validity remain more important.

Tie-breakers:

1. More likely to start.
2. More likely to play 60+ minutes.
3. Better current-day or current-tournament metrics.
4. Stronger team matchup.
5. Stronger role for fantasy scoring by position.
6. Lower card or own-goal risk.
7. Smaller amount of missing metadata.
8. Host nation or home-like advantage, if present.
9. Differentiated pick, only if candidates remain close after the prior tie-breakers.

Fallback:

If data is sparse, select the safest valid lineup by prioritizing clear eligibility, position coverage, prior starts, prior minutes, and players from stronger teams in that day's fixtures.
