---
name: final-answer-guardrails
description: Validate the final answer shape, IDs, and runtime behavior before returning JSON.
---

Use this skill before returning the final answer.

Primary objective:
Return one plain JSON object that matches the tournament answer contract.

Required top-level keys:

- `team_id`
- `matchday_id`
- `fantasy_xi`
- `risk_play`
- `strategy`

Output rules:

1. Return plain JSON only.
2. Do not wrap the answer in Markdown fences.
3. Do not include explanatory text outside JSON.
4. Do not include extra top-level keys unless the schema in `output-format/` explicitly requires them.
5. Do not include `bet_points`, `stake`, or `stake_percent`.
6. Use the team and matchday IDs from the prompt and official game board.

Fantasy XI validation:

1. `fantasy_xi` must contain exactly 11 player IDs.
2. All 11 IDs must be unique.
3. Every selected ID must exist in `game-board/players.json`.
4. Every selected player must be eligible for the current day.
5. The formation must contain exactly 1 GK, 3 to 5 DEF, 3 to 5 MID, and 1 to 3 FWD.
6. If the first selected lineup fails validation, repair the lineup before answering.

Risk Play validation:

1. `risk_play` must be either `null` or a valid claim object from the current claim catalog.
2. The claim object must include the required fields for its `claim_id`.
3. Match IDs, team IDs, and player IDs must come from the current daily board.
4. Team and player fields must belong to the submitted match.
5. If any Risk Play field is uncertain, invalid, or unsupported, use `null`.

Runtime guardrails:

1. Finish within 5 minutes.
2. Do not install packages.
3. Do not run scripts.
4. Do not write, edit, delete, or move files.
5. Do not depend on private systems, credentials, browser cookies, VPN-only resources, authenticated services, or external network access.
6. Do not wait for manual user or organizer action.
7. If any optional context is slow, unavailable, conflicting, or unnecessary, ignore it and rely on the official game board.

Strategy text:

Keep `strategy` brief. Mention the main lineup logic, the risk posture, and any important uncertainty. Do not reveal hidden reasoning or include long analysis.

Final check:

Before returning, re-read the output schema/examples in `output-format/` if available and make the answer conform to them exactly.
