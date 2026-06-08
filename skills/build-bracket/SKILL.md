---
name: build-bracket
description: Make bracket picks during knockout phases when the tournament asks for them.
---

Use this skill only when bracket play is open and the daily prompt or `game-board/bracket.json` asks for bracket picks.

Primary objective:
Submit valid bracket picks using the current bracket board and organizer instructions.

Source-of-truth rules:

1. Read `prompt.md`, `rules/`, `output-format/`, and `game-board/bracket.json`.
2. Use only match IDs, team IDs, and pick fields present in the current bracket board.
3. Follow organizer lock rules and required pick sets exactly.
4. Do not include bracket picks when the prompt does not request them.

Bracket strategy:

1. Prefer teams with stronger tournament performance, stronger goal differential, better defensive record, and more reliable attacking output when those fields are available.
2. Prefer teams with healthier or more stable likely starters when that information is present in the board.
3. Give a small boost to host nations or teams with clear home-like context if the board supports it.
4. In close matchups, prefer the team with stronger knockout reliability indicators if available.
5. Do not overfit to old historical reputation when current tournament data points the other way.

Risk posture:

1. Bracket champion and late-round picks are high leverage. Choose teams with a credible path, not just one favorable match.
2. If standings context shows the fantasy team is far behind and bracket scoring is still open, modest contrarian picks are acceptable.
3. If standings context is strong or unclear, prefer higher-probability picks.

Fallback:

If bracket data is missing, incomplete, or not requested, do not fabricate bracket picks. Continue with the daily Fantasy XI and Risk Play answer only.
