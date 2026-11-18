# Back-end rules

## Back-end code changes — always delegate to the `backend-workflow` sub-agent

Every back-end change (new feature, bug fix or refactoring in `app-backend/`) MUST go through the `backend-workflow` sub-agent, via the Agent tool. Don't write production or test code or update the OpenAPI spec yourself.

Pass the requested change to the sub-agent in your own words. Outside an epic build, if it needs a new REST host, include a descriptive service name that is a valid C# identifier. The sub-agent runs the whole cycle without stopping for approvals and returns a summary once it is green and refactored; then follow the gate below.

## Manual testing & committing a completed cycle

Committing is part of the main process, not the sub-agent. During an epic build, `/continue` handles this. Otherwise, when the sub-agent returns a completed cycle:

1. **STOP. Do not stage or commit anything yet.** Ask the user to confirm they've manually tested the feature, bug fix or refactoring, and wait for their explicit confirmation.
2. Stage all changes from the cycle (production and test code, plus `transcript-collection.json` if it exists at the repo root) and commit with a concise message describing the change.
3. Only then re-invoke the sub-agent for the next cycle.
