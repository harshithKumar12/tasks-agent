# Daily Task Agent

A single-notebook, natural-language task agent. You type a request in plain
English; the notebook parses the intent, routes it to a tool function, and
persists tasks and reminders to a local JSON file.

## Features

- **Intent parsing** — `add_task`, `set_reminder`, `list_tasks`, `delete_task`,
  `mark_done`, `clear`, `help`.
- **Date/time extraction** — phrases like `tomorrow at 7 PM`, `on Friday at
  10 AM`, or `in 30 minutes` (`dateparser` when installed, with a built-in
  regex fallback otherwise).
- **Local JSON storage** — under `~/.daily_task_agent/tasks.json`, overridable
  with the `TASK_AGENT_HOME` environment variable.
- **Pluggable tools** — a `TOOL_REGISTRY` so a calendar or notification backend
  can be swapped in later.

## Run it

Open `daily_agent.ipynb` in Jupyter and run the cells top to bottom, then:

```python
agent.handle("Remind me to study DSA tomorrow at 7 PM.")
agent.handle("What tasks do I have today?")
```

The final cell starts an interactive REPL (`quit` to leave).

Optional enhancement:

```bash
pip install dateparser
```

## Layout

| Cell section | Responsibility |
| --- | --- |
| Storage | JSON persistence for tasks and reminders |
| NLP | Intent detection and entity extraction |
| Tools | `add_task`, `list_tasks`, `set_reminder`, `mark_done`, `delete_task` |
| Agent | Routes parsed intents to tools and formats replies |
| Demo / REPL | Example prompts and an interactive loop |

## Notes

- Data is written atomically via a temp file and rename.
- The notebook is self-contained; it has no package or test suite.
