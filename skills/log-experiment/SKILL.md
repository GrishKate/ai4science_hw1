---
name: log-experiment
description: Log a completed VideoQA experiment in results/ and memory/experiments_graph.md according to ontology.yaml. Use after a local, Kaggle, or other evaluation run produced metrics; also use when importing existing run artifacts. 
---

# Логирование эксперимента

Считай `ontology.yaml` и `ontology/*.md` источником истины. Один эксперимент — один запуск с фиксированными кодом, конфигурацией и оборудованием. Изменение любого из них создаёт новый эксперимент.

## Перед записью

Собери обязательные значения:

- уникальный `experiment_id`;
- точное название `hardware`;
- `method_id` и краткое содержательное описание метода;
- полный 40-символьный lowercase Git `commit_hash` состояния кода при запуске;
- фактический YAML-конфиг со всеми гиперпараметрами;
Полученный CSV со всеми метриками может быть скачан позже пользователем. Сохрани все остальные параметры запуска, кроме CSV, если он недоступен.

Не подменяй неизвестные значения догадками. Если обязательного значения или файла нет, сообщи, что эксперимент пока нельзя зарегистрировать как воспроизводимый. Не создавай фиктивные метрики и не записывай незавершённый запуск в граф как завершённый эксперимент.

До любых изменений проверь, что `experiment_id`, `measurement_id` и `results/<experiment_id>/` ещё не используются. Никогда не изменяй и не перезаписывай существующие файлы в `results/`. При коллизии выбери новый идентификатор только вместе с пользователем.

## Файлы результата

Создай отдельный каталог:

```text
results 
├── method.yaml
results/<experiment_id>/
├── experiment.yaml
├── metrics.csv
├── runner.yaml
```
- `method.yaml` — краткое содержательное описание метода, формат в `ontology/method.md`. Может переиспользоваться.
- `experiment.yaml` — описание запуска метода, формат в `ontology/experiment.md`.
- `metrics.csv` — исходный файл метрик запуска. Если файл доступен, сохрани все столбцы и строки; не заменяй его пересказом или агрегатами. Если файл сейчас не доступен, не сохраняй его, пользователь сам позже сохранит.
- `runner.yaml` — аргументы командной строки для запуска, формат в `ontology/runner.md`.


## Реестр `memory/experiments_graph.md`
Добавь в граф знаний в `memory/experiments_graph.md` запись о запущенных экспериментах.

Если `method_id` отсутствует в разделе `## Методы`, добавь ровно одну строку:

```markdown
| <method_id> | <description> |
```

В раздел `## Эксперименты` добавь запись, содержащую только эти поля сущности `Experiment`:

```markdown
### <experiment_id>
- **experiment_id:** <experiment_id>
- **results_directory:** results/<experiment_id>/
- **method:** <method_id>
```

Не копируй отдельные значения метрик или гиперпараметры в эту запись.

В разделе `## Измерения` (создай его перед `## Связи`, если раздела ещё нет) добавь сущность `Measurement`:

```markdown
### <experiment_id>_metrics
- **measurement_id:** <experiment_id>_metrics
- **metrics_file:** results/<experiment_id>/metrics.csv
```

В раздел `## Связи` добавь строки:

```text
Method:<method_id> ──exp──> Experiment:<experiment_id> ──measures──> Measurement:<experiment_id>_metrics
Experiment:<experiment_id> ──uses──> Runner:<experiment_id>_runner
```

## Журнал и проверка

Добавь в конец `memory/diary.md` датированную запись с запросом, созданными артефактами, результатом, точкой проверки и итогом проверки. Не включай секреты или содержимое файлов с ключами.

