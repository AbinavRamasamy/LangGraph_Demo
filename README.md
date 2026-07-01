# LangGraph_Demo

LangGraph calculator example: a router node conditionally branches to an operation node (add, subtract, multiply, divide, modulo, exponent), converges to a message node, and falls back to `END` on an unknown operator. Graph visualized via `IPython.display`.

## Setup

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Copy `.env.example` to `.env` and set `OPENROUTER_API_KEY` if you plan to use an LLM into any of the nodes.

## Run

Open `langgraph.ipynb` and run all cells (kernel: `.venv`).

Or execute headless:

```bash
jupyter nbconvert --to notebook --execute --inplace langgraph.ipynb
```

## How it works

- `AgentState` (TypedDict) holds `num1`, `operator`, `num2`, `result`, `message`.
- `router` node fills in any missing state keys with defaults before routing.
- `add_conditional_edges` sends state to the matching operation node based on `operator`; unrecognized operators route straight to `END`.
- Each operation node computes `result`; all converge on a `create_message` node that formats the final string.

## Project structure

```
langgraph.ipynb     # notebook: graph definition, visualization, and a sample invoke
requirements.txt    # dependencies
```
