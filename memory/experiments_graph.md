## Методы

| method_id | description |
|---|---|
| baseline | Qwen3-VL reference evaluation without visual-token pruning. |
| dart | DART visual-token pruning using image and text pivots to retain tokens relevant to multimodal generation. |
| fastv | FastV-style visual-token pruning based on attention from the last text token. |

## Эксперименты

### baseline_r0.75_mvbench_action_count_2026-10-18_kaggle_v11
- **experiment_id:** baseline_r0.75_mvbench_action_count_2026-10-18_kaggle_v11
- **results_directory:** results/baseline_r0.75_mvbench_action_count_2026-10-18_kaggle_v11/
- **method:** baseline

### dart_r0.75_mvbench_action_count_2026-10-18_kaggle_v11
- **experiment_id:** dart_r0.75_mvbench_action_count_2026-10-18_kaggle_v11
- **results_directory:** results/dart_r0.75_mvbench_action_count_2026-10-18_kaggle_v11/
- **method:** dart

### fastv_r0.75_mvbench_action_count_2026-10-18_kaggle_v11
- **experiment_id:** fastv_r0.75_mvbench_action_count_2026-10-18_kaggle_v11
- **results_directory:** results/fastv_r0.75_mvbench_action_count_2026-10-18_kaggle_v11/
- **method:** fastv

## Измерения

### baseline_r0.75_mvbench_action_count_2026-10-18_kaggle_v11_metrics
- **measurement_id:** baseline_r0.75_mvbench_action_count_2026-10-18_kaggle_v11_metrics
- **metrics_file:** results/baseline_r0.75_mvbench_action_count_2026-10-18_kaggle_v11/metrics.csv

### dart_r0.75_mvbench_action_count_2026-10-18_kaggle_v11_metrics
- **measurement_id:** dart_r0.75_mvbench_action_count_2026-10-18_kaggle_v11_metrics
- **metrics_file:** results/dart_r0.75_mvbench_action_count_2026-10-18_kaggle_v11/metrics.csv

### fastv_r0.75_mvbench_action_count_2026-10-18_kaggle_v11_metrics
- **measurement_id:** fastv_r0.75_mvbench_action_count_2026-10-18_kaggle_v11_metrics
- **metrics_file:** results/fastv_r0.75_mvbench_action_count_2026-10-18_kaggle_v11/metrics.csv

## Связи

Method:baseline ──exp──> Experiment:baseline_r0.75_mvbench_action_count_2026-10-18_kaggle_v11 ──measures──> Measurement:baseline_r0.75_mvbench_action_count_2026-10-18_kaggle_v11_metrics
Experiment:baseline_r0.75_mvbench_action_count_2026-10-18_kaggle_v11 ──uses──> Runner:baseline_r0.75_mvbench_action_count_2026-10-18_kaggle_v11_runner

Method:dart ──exp──> Experiment:dart_r0.75_mvbench_action_count_2026-10-18_kaggle_v11 ──measures──> Measurement:dart_r0.75_mvbench_action_count_2026-10-18_kaggle_v11_metrics
Experiment:dart_r0.75_mvbench_action_count_2026-10-18_kaggle_v11 ──uses──> Runner:dart_r0.75_mvbench_action_count_2026-10-18_kaggle_v11_runner

Method:fastv ──exp──> Experiment:fastv_r0.75_mvbench_action_count_2026-10-18_kaggle_v11 ──measures──> Measurement:fastv_r0.75_mvbench_action_count_2026-10-18_kaggle_v11_metrics
Experiment:fastv_r0.75_mvbench_action_count_2026-10-18_kaggle_v11 ──uses──> Runner:fastv_r0.75_mvbench_action_count_2026-10-18_kaggle_v11_runner
