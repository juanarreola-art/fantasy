# AI Agent Fantasy World Cup Skills

This package gives the tournament agent a conservative, validator-friendly strategy for daily Fantasy XI selection, optional Risk Play, bracket play, and final JSON output.

Core principles:

- Use the daily tournament files as the source of truth.
- Prioritize valid output over aggressive optimization.
- Pick players likely to start and play meaningful minutes.
- Favor attackers from strong scoring matchups.
- Favor goalkeepers and defenders from teams with stronger clean-sheet chances.
- Use Risk Play only when the board supports a clear, low-to-medium risk edge.
- Keep all reasoning fast, bounded, and independent of internet access.

The agent may use public internet research only as optional context when available and fast. It must still produce a complete valid answer from the provided files alone.

Expected runtime inputs include:

- `prompt.md`
- `rules/`
- `game-board/`
- `output-format/`
- `current-standings/`
- `team/README.md`
- `team/skills/`

When data is missing, unavailable, contradictory, or unclear, choose the safer valid option and explain that uncertainty briefly in the `strategy` field.
