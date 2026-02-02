# TRP1 – Tenx MCP Setup (Cursor)

This repository contains my work for the **TRP1 – MCP Setup Challenge**, focused on configuring the **Tenx MCP Analysis** server in **Cursor**, defining effective agent rules, and documenting the process.

## What this repo contains

- `.cursor/mcp.json`  
  Tenx MCP server configuration for Cursor:

  - Server name: `tenxfeedbackanalytics`
  - URL: `https://mcppulse.10academy.org/proxy`
  - Headers:
    - `X-Device: "linux"`
    - `X-Coding-Tool: "cursor"`

- `.cursor/rules/agent.mdc`  
  Agent rules that:

  - Enforce the **Tenx logging workflow**:
    - Call `log_passage_time_trigger` on **every** user message.
    - Call `log_performance_outlier_trigger` when performance patterns (efficient / inefficient / stalled) are detected.
    - Show performance feedback at the end of each answer, wrapped in `*****************************************` and starting with `Analysis Feedback: ...`, while **hiding** the `log_passage_time_trigger` output.
  - Define **general collaboration behavior**:
    - Agent behaves like a **senior pair‑programmer**.
    - Plans before making large changes; keeps responses concise and structured.
    - Bias toward **modern JavaScript/TypeScript** for examples and style.
  - Include **coding style, testing, safety, and communication** guidelines:
    - Modern JS/TS (ES modules, `const`/`let`, async/await, arrow functions, TypeScript for new code when possible).
    - Suggest at least one way to test new/changed logic.
    - Avoid destructive actions unless explicitly requested.
    - Use focused code snippets and minimal noise.

- `TRP1-report.md`  
  A written report covering:
  - **What I did** (MCP setup in Cursor, rules configuration).
  - **What worked** and **what didn’t**.
  - **Insights** on how rules change agent behavior and align it with my way of thinking.
  - Possible next steps for further refinement.

## How to use this setup (Cursor)

1. **Open this project in Cursor.**
2. Ensure Cursor is up to date (latest version).
3. Verify `.cursor/mcp.json` and `.cursor/rules/agent.mdc` exist (as in this repo).
4. In Cursor:
   - Open the **MCP servers panel**.
   - Enable the **`tenxfeedbackanalytics` / `tenxanalysismcp`** server.
   - Click **Connect** and authenticate with GitHub when prompted.
5. Start a new chat in this workspace and interact normally.  
   - Tenx MCP logging runs **in the background**.
   - The agent follows the rules in `agent.mdc` for both Tenx triggers and general coding behavior.

## Notes and learnings

- A well‑designed rules file significantly changes how the agent behaves:
  - Less repetitive prompting.
  - More consistent planning, testing suggestions, and safety checks.
- Separating **Tenx‑specific logging rules** from **general development guidance** makes it easier to adjust each part independently.
- The setup is intentionally lightweight so it can be extended later (for example, adding framework‑specific rules for React, Node, or other stacks).