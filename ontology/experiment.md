# Experiment

`Experiment` описывает один воспроизводимый запуск метода. Повторный запуск с
другим оборудованием, конфигурацией или состоянием кода считается новым
экспериментом.

## Поля

| Поле | Тип | Обязательное | Назначение |
|---|---|---:|---|
| `experiment_id` | `string` | да | Уникальный идентификатор запуска |
| `hardware` | `string` | да | Оборудование, например `NVIDIA Tesla T4` |
| `config_file` | `path` | да | YAML-файл с гиперпараметрами запуска |
| `commit_hash` | `string` | да | Полный 40-символьный Git commit hash |
| `results_directory` | `path` | да | Отдельная папка запуска внутри `results/` |
| `method` | `Method` | да | Метод, использованный при запуске |
| `measurement` | `Measurement` | да | Набор полученных метрик |
| `runner` | `Runner` | да | Аргументы командной строки с которыми выполнен запуск |

Один эксперимент связан ровно с одним методом и одним набором измерений. Один
метод может использоваться во многих экспериментах.

## Пример

```yaml
experiment_id: quietprune_2026_10_12
hardware: NVIDIA Tesla T4
config_file: src/angelslim/configs/qwen3_vl/quietprune.yaml
commit_hash: c5f8d71cdfb367c69dd2e45bc7fd9122d7090d38
results_directory: results/12-10/
method: quietprune
measurement: quietprune_2026_10_12_metrics
runner: quietprune_2026_10_12
```

Папка результата считается неизменяемой: следующий запуск должен получить
новый `experiment_id` и новую папку, а не перезаписать существующую.
