# Agent Loop — Built From Scratch

A raw OpenAI agent loop built from first principles — no frameworks, no LangChain, just the OpenAI API and Python.

## What This Is

Most AI agent courses use LangChain or the OpenAI Agents SDK which hide the agent loop behind abstractions. This project implements that loop manually to show exactly what's happening underneath every framework.

The agent solves a problem by:
1. Breaking it into steps using a todo list
2. Carrying out each step using tool calls
3. Returning a final answer in Rich console markup

## How The Agent Loop Works

```
Send messages to GPT
    ↓
GPT wants to call a tool?  →  run the tool, add result to messages, loop again
    ↓
GPT is done?  →  return the final answer
```

The key is `finish_reason`. When GPT returns `"tool_calls"` it wants to run a function. When it returns `"stop"` it's done. That's the entire loop.

## Tools

**`create_todos(descriptions: list[str])`**
Creates a list of steps for the agent to work through. Returns the full todo list.

**`mark_complete(index: int, completion_notes: str)`**
Marks a step as done and records completion notes. Returns the updated list.

## Stack

- Python
- OpenAI API `gpt-4o-mini`
- Rich — terminal formatting
- python-dotenv — API key management

## Setup

Requires [uv](https://docs.astral.sh/uv/) — install it first if you don't have it:

```bash
pip install uv
```

Clone and set up the project:

```bash
git clone https://github.com/agenticmohit/agent-loop-from-scratch
cd agent-loop-from-scratch
uv venv
source .venv/bin/activate        # Mac/Linux
.venv\Scripts\activate           # Windows
uv add openai rich python-dotenv
```

Create a `.env` file:

```
OPENAI_API_KEY=your_key_here
```

Run:

```bash
python agent_loop.py
```

## Sample Output

The agent solves a train timing problem by creating todo steps for each calculation, marking them complete as it works through them, then returning a formatted final answer in the terminal.

## Why I Built This

Understanding what happens inside `agent.invoke()` or `Runner.run()` makes you a better AI engineer. This is the raw loop — the internals every framework is built on top of.

---

Part of my AI engineering learning path. See also:
- [Reelioo](https://github.com/agenticmohit/reelioo) — agentic crypto intelligence terminal
- [Forge](https://github.com/agenticmohit/forge-local-ai-agent) — local AI coding agent