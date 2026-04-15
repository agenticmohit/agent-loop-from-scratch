# Agent Loop — Built From Scratch

A raw OpenAI agent loop built from first principles — no frameworks, no LangChain, just the OpenAI API and Python.

## What This Is

Most AI agent courses use LangChain or the OpenAI Agents SDK which hide the agent loop behind abstractions. This project implements that loop manually to show exactly what's happening underneath every framework.

The agent solves a multi-step crypto price calculation by:
1. Breaking the problem into steps using a todo list
2. Carrying out each calculation step using tool calls
3. Returning a formatted final answer in the terminal

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
Creates a list of calculation steps for the agent to work through. Returns the full todo list.

**`mark_complete(index: int, completion_notes: str)`**
Marks a step as done and records the result. Returns the updated list.

## The Problem

```
A crypto trader buys Bitcoin at $42,000.
It drops 15% the first week, then rises 22% the second week.
What is the current price and the net percentage gain or loss?
```

The agent plans its own steps, calculates each one, and returns the final answer — no hardcoded logic, just GPT reasoning with tools.

## Stack

- Python
- OpenAI API `gpt-5.2`
- Rich — terminal formatting
- python-dotenv — API key management

## Setup

Requires [uv](https://docs.astral.sh/uv/). Install it if you don't have it:

```bash
pip install uv
```

Clone the repo and install dependencies:

```bash
git clone https://github.com/agenticmohit/agent-loop-from-scratch
cd agent-loop-from-scratch
uv sync
```

Create a `.env` file:

```
OPENAI_API_KEY=your_key_here
```

Run:

```bash
uv run main.py
```

## Sample Output

The agent creates todo steps — calculate price after week 1 drop, calculate price after week 2 rise, calculate net change — marks each complete with the result, then returns a formatted terminal summary.

## Why I Built This

Understanding what happens inside `agent.invoke()` or `Runner.run()` makes you a better AI engineer. This is the raw loop — the internals every framework is built on top of.

---

Part of my AI engineering learning path. See also:
- [Reelioo](https://github.com/agenticmohit/reelioo) — agentic crypto intelligence terminal
- [Forge](https://github.com/agenticmohit/forge-local-ai-agent) — local AI coding agent