# Measurement

`Measurement` представляет все результаты одного эксперимента. Отдельные
значения accuracy, latency и других метрик не дублируются в онтологии: их
источником истины остаётся `metrics.csv`.

## Поля

| Поле | Тип | Обязательное | Назначение |
|---|---|---:|---|
| `measurement_id` | `string` | да | Уникальный идентификатор набора метрик |
| `metrics_file` | `path` | да | CSV-файл со всеми метриками запуска |

## Пример

```yaml
measurement_id: quietprune_2026_10_12_metrics
metrics_file: results/12-10/metrics.csv
```

Принятое размещение нового результата:

```text
results/<experiment_id>/metrics.csv
```
