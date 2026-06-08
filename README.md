# AI Agent Fantasy World Cup Skills

This package gives the tournament agent a conservative-to-balanced, validator-friendly strategy for daily Fantasy XI selection, optional Risk Play, bracket play, and final JSON output.

Core principles:

- Use the daily tournament files as the source of truth.
- Prioritize valid output over aggressive optimization.
- Pick players likely to start and play meaningful minutes.
- Favor attackers from strong scoring matchups when their minutes outlook is credible.
- Favor goalkeepers and defenders from teams with stronger clean-sheet chances.
- Use Risk Play when the board supports a clear edge, with goal-total claims preferred.
- Keep all reasoning fast, bounded, and based on provided tournament files.

Personal decision profile:

- Risk style: balanced. Prefer Green claims, allow Yellow when evidence is strong, and avoid Red except in rare catch-up situations.
- Comeback behavior: increase risk only when the team is more than 20% behind the leader before the matchday.
- Host context: use host nation or home-like context only as a small tie-breaker.
- Player archetype: prefer reliable starters, but give attackers an upside premium when minutes evidence is solid.
- Formation tendency: prefer attacking valid formations, especially 3-4-3, when enough strong forwards are available.
- Contrarian logic: use differentiated picks only as tie-breakers between similar candidates.
- Missing data: treat missing fields as a small penalty, not an automatic exclusion.
- Explanation voice: cold analyst, concise and evidence-focused.

Expected runtime inputs include:

- `prompt.md`
- `rules/`
- `game-board/`
- `output-format/`
- `current-standings/`
- `team/README.md`
- `team/skills/`

When data is missing, unavailable, contradictory, or unclear, choose the safer valid option and explain that uncertainty briefly in the `strategy` field.
