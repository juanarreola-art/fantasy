---
name: choose-risk-play
description: Choose at most one valid Risk Play using a conservative stake-aware policy.
---

Use this skill when deciding whether to submit a Risk Play.

Primary objective:
Choose one valid Risk Play only when the daily board supports a clear edge. Otherwise return `risk_play: null`.

Source-of-truth rules:

1. Read `game-board/claim-catalog.json` before choosing a claim.
2. Read `game-board/matches.json`, `game-board/players.json`, `game-board/teams.json`, and `game-board/standings-before.json`.
3. Submit only claim IDs and required fields that exist in the current daily board.
4. For team claims, use a team that belongs to the submitted match.
5. For player claims, use a player who belongs to one of the submitted match teams and is present in the current board.
6. Do not invent stake, `bet_points`, or `stake_percent`. The tournament computes stake.

Risk posture:

1. Skipping Risk Play is valid and often correct.
2. Prefer Green claims when confidence is moderate or data is incomplete.
3. Use Yellow claims only when the board provides strong supporting evidence.
4. Avoid Red claims unless the evidence is exceptional and the standings context clearly rewards high risk.
5. If team points before the matchday are 0 or less, return `risk_play: null`.

Default preferred Green claims:

1. `match_2plus_goals` when both teams have reasonable scoring indicators or the matchup looks open.
2. `goal_before_halftime` when at least one team has strong attacking indicators and likely starters.
3. `match_2plus_cards` when teams or matchup context suggest physical play and card data supports it.
4. `no_goal_first_10` only when both teams appear cautious or low-scoring.
5. `no_goal_stoppage_time` only as a low-information fallback if other Green claims lack support.

Yellow claim guidance:

1. `both_teams_score` requires evidence that both teams can score.
2. `match_over_2_5_goals` requires stronger evidence than `match_2plus_goals`.
3. `team_scores_first` requires a clearly stronger attacking team in the match.
4. `player_scores` requires a likely starter with strong goal-scoring role.
5. `match_2plus_yellow_cards` requires card-specific support.

Red claim guidance:

1. `exact_score` is usually too risky. Avoid by default.
2. `player_scores_2plus` is usually too risky. Use only for an elite scorer in an extremely favorable matchup.
3. `team_wins_by_3plus` requires a major team-strength mismatch.
4. `team_comeback_win` is too specific. Avoid by default.
5. `red_card_shown` requires strong card or rivalry evidence.
6. Extra-time and penalty claims are relevant only in knockout matches and require match phase support.

Standings-aware adjustment:

1. If the team is near the top of standings, prefer Green or skip.
2. If the team is in the middle, prefer Green and use Yellow only with strong evidence.
3. If the team is far behind late in the tournament, consider Yellow or rare Red claims only when evidence is strong.
4. Do not take high risk merely because it is available.

Fallback:

If claim support is unclear, fields cannot be validated, team/player IDs do not align cleanly with the match, or time is running short, return `risk_play: null`.
