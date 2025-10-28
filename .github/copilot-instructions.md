## Copilot instructions for movie_analyst_project

Purpose
- Help AI coding agents make small, safe, high-value changes in this repository.

Quick context
- This is a small Python analysis project. The repository root contains:
  - `analysis.py` — main analysis script (currently minimal/empty).
  - `requirements.txt` — pinned runtime dependencies (pandas, numpy, matplotlib, seaborn, etc.).

What to do first (environment)
- Use Windows PowerShell commands to prepare the environment:
  - Create a venv and install deps: `python -m venv .venv; .\\.venv\\Scripts\\Activate.ps1; pip install -r requirements.txt`.
- Quick smoke check after install: try importing critical libs (`pandas`, `matplotlib`, `seaborn`) to catch missing deps.

Project-specific coding patterns
- Single-script entry: keep the top-level script (`analysis.py`) thin. Prefer creating small, pure functions that accept inputs (e.g., pandas.DataFrame or file paths) and return results (DataFrame, figure, numeric summary) rather than performing side-effects directly.
- Plotting: functions that produce visuals should return `(fig, ax)` or `matplotlib.figure.Figure` so callers/tests can inspect or save the output.
- Data I/O convention: code in this repo expects to operate on tabular data (pandas). When adding parsing helpers, accept either a path or an already-loaded DataFrame.
- Dependencies: always add new runtime libraries to `requirements.txt` (pinned) and mention the change in the commit message.

Examples the agent can use
- When adding a reusable function, place it in `analysis.py` (project is small - keep related helpers nearby). Example intent: "Add function `load_ratings(path: str) -> pd.DataFrame` that reads a CSV and normalizes column names."
- When adding plotting helpers, return `(fig, ax)` and avoid calling `plt.show()` inside the helper.

Testing and verification
- This repo currently has no test harness. Before opening a PR, run a quick smoke test by importing the new symbols:
  - `python -c "import analysis; print('OK')"`
- Run a small data-driven smoke: after adding a loader, run it on a small CSV fixture and assert the returned DataFrame has expected columns.

Agent constraints
- Avoid large refactors without an explicit user request - this is a tiny single-script project. Prefer incremental, well-documented changes.
- When adding files, update `requirements.txt` if you introduce new runtime dependencies.

What to mention in PR descriptions
- Brief summary of the change (1-2 lines).
- Files modified and why.
- Any new dependency added and reason.

If you can't find data files
- This repo does not include datasets. If you add code that expects files, either: include a small CSV fixture in a `tests/fixtures` folder or make the function accept a DataFrame so it can be unit-tested without on-disk data.

Questions for the repo owner
- Preferred location for helper modules if this grows beyond a single file (e.g., `src/` vs root)?
- Do you want automated tests added to a specific framework (pytest suggested)?

End of file
