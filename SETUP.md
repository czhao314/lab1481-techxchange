# Setup & Installation

This project requires **Python 3.12.10** and uses `pyproject.toml` to declare its dependencies.

---

## Prerequisites

Install [`uv`](https://github.com/astral-sh/uv) if you don't have it already:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

---

## Install dependencies

```bash
uv sync
```

`uv sync` reads `pyproject.toml`, creates a virtual environment (`.venv`) pinned to Python 3.12.10, and installs all declared dependencies in one step.

To activate the environment afterwards:

```bash
source .venv/bin/activate        # macOS / Linux
# .venv\Scripts\activate         # Windows
```

---

## Installed packages

| Package | Description |
|---------|-------------|
| `cplex` | IBM CPLEX optimisation solver |
| `docplex` | Python modelling API for CPLEX |
| `requests` | HTTP library |
| `pandas` | Data analysis and manipulation |
| `ibm-watsonx-ai` | IBM watsonx.ai Python SDK |
| `numpy` | Numerical computing |

---

## Notes

- `os`, `sys`, `subprocess`, `importlib`, `base64`, and `time` are part of the Python standard library and do not need to be installed separately.
- If you encounter issues installing `cplex`, ensure you have a valid IBM CPLEX licence. The community edition can be installed via `pip install cplex`.
