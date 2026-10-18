# Runner

`Runner` сохраняет аргументы командной строки с которыми выполнялся запуск эксперимента.

## Поля

| Поле | Тип | Обязательное | Назначение |
|---|---|---:|---|
| `experiment_id` | `string` | да | Идентификатор эксперимента |
| `script` | `string` | да | Файл для запуска |

Пример ниже содержит только некоторые поля, нужно записывать в yaml файл все переданные аргументы.

## Пример

```yaml
experiment_id: quietprune_2026_10_12
script: src/run_evaluation.py
model_path: "./qwen3_vl_debug"
task: "mvbench"
dtype: "float16"
config: "src/angelslim/configs/qwen3_vl/quietprune.yaml"
max_tokens: 10
limit: 0.01
```
