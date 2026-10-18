---
name: run-in-kaggle
description: Run project evaluations in a configured Kaggle notebook, monitor execution, retrieve logs and outputs, and record reproducible results.
---

# Run tests on Kaggle

Use the Kaggle CLI to synchronize and execute the project's configured evaluation notebook.

## Preconditions

- Require a notebook handle in the form `owner/notebook-slug`.
- Require the `kaggle` CLI to be installed and authenticated.
- Never read, display, copy, or commit Kaggle credentials.
- Keep notebook sources under `notebooks/`.
- Keep downloaded run artifacts under `results/outputs/`.

If authentication or network access is unavailable, report the exact missing
precondition. Do not ask the user to paste a token into chat.

## Workflow
0. Run `source /Users/grish-kate/Desktop/VscodeProjects/agent_instance/AI4Science/.venv/bin/activate`.
1. Pull the latest notebook source and metadata before editing:
   `kaggle kernels pull <handle> -p <notebook-directory> --metadata`.
2. Preserve unrelated notebook cells and metadata.
3. Apply only changes required for the requested evaluation.
4. Show the user which local files changed before uploading.
5. Treat `kaggle kernels push` as an external mutation. Obtain any approval
   required by the current environment immediately before pushing.
6. Push the notebook directory to create and run a new version.
7. Poll `kaggle kernels status <handle>` until completion or the agreed timeout (5 minutes).
8. On failure, retrieve `kaggle kernels logs <handle>` and report the relevant
   error without exposing secrets.
9. Ater timeout of 5 minutes stop waiting, report to user that notebook has started and finish. 
10. On success, download outputs with
   `kaggle kernels output <handle> -p <output-directory>`. Download the expected files with metrics to `results/` in folder `<experiment_name>_<date>`, add `description.md` file with short description. Do not rewrite existing files in `results/`.
10. Record the run and verification point in `diary.md`. 

Do not delete Kaggle notebooks or datasets. Do not repeatedly submit failed
runs without diagnosing the failure.