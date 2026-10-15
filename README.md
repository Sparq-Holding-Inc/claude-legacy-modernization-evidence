# Legacy Modernization Assessor: eval evidence

The saved runs behind the scorecard of the
[Legacy Modernization Assessor](https://github.com/Sparq-Holding-Inc/claude-legacy-modernization) plugin.

They live here, not in the plugin repo, so the plugin repo holds only what the plugin runs and the
code that tests it. Nothing in this repo is loaded by the plugin.

## What is here

| Path | What it is |
|---|---|
| `runs/<case>/` | One end to end run per fixture and three CardDemo runs: the assessment the plugin wrote (`modernization-assessment/`), the `claude -p` result with cost and turns, and how the run was started (`run-meta.json`). |
| `real-harness/11-dead-program/` | The first trial of the headless harness on one fixture, kept for its cost lesson. |
| `examples/carddemo/graph.json` | The full graph for the sample assessment in the plugin repo's `examples/carddemo/`. |

## How the runs were produced

On 2026-10-14, through `claude -p` with `--plugin-dir` pointing at the plugin. Model: Claude Sonnet 5.5.

- The 13 fixture runs used plugin commit `91cdfe2`.
- The 3 CardDemo runs were repeated after the wave seed change. They used the working tree that was
  committed as `a50b16d`.

The plugin repo's `evals/scorecard/e2e-provenance.json` has the details and what the harness did not
exercise.

These files were copied byte for byte from the plugin repo at commit `229de03`, where they were under
`evals/runs/`, `evals/real-harness/` and `examples/carddemo/`. Their history up to that commit is in the
plugin repo.

Local paths in the saved runs were replaced with `<workspace>` (the folder that holds the plugin checkout)
and `<home>`.

## Score them

Clone this repo next to the plugin repo, then score from the plugin repo:

```bash
git clone https://github.com/Sparq-Holding-Inc/claude-legacy-modernization
git clone https://github.com/Sparq-Holding-Inc/claude-legacy-modernization-evidence
cd claude-legacy-modernization
python3 evals/run_e2e_evals.py --score-only
```

The scorer looks for this repo at `../claude-legacy-modernization-evidence`. Pass `--evidence DIR` if it
is somewhere else.

Citations point into the source tree each run assessed, its work folder at `../bench/runs/<case>/work`.
`python3 evals/run_e2e_evals.py --prepare` rebuilds those folders from the fixtures and from a CardDemo
checkout at `../bench/carddemo` (see `evals/carddemo/SOURCE.md` in the plugin repo for the pinned commit).
It does not touch the saved runs. Without the work folders, citations into the source count as unresolved.

## License

Apache-2.0. See `LICENSE` and `NOTICE`.
