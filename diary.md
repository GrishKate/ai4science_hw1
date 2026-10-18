## 2026-10-09

- Запрос: исправить обработку видео при pruning в `qwen3_vl/vl_model.py` по аналогии с корректной обработкой изображений; тесты не запускать.
- Сделано: video-ветка переведена на batch-aware `vit_kept_positions`, добавлены register spaces и padding для `input_ids`/`inputs_embeds`.
- Результат: удалено boolean-индексирование, рассчитанное только на batch size 1; видео теперь использует тот же путь изменения длины, что и изображения.
- Точка проверки: `src/angelslim/compressor/token_compressor/qwen3_vl/vl_model.py`, блок `pixel_values_videos`.
- Итог проверки: тесты не запускались по прямому указанию пользователя.

## 2026-10-17
- **Запрос:** Дополнить frame_sampling.md описаниями из OpenAlex.
- **Что сделано:** Поиск 10 статей в OpenAlex по названию, получение полных записей с аннотациями. Заполнены openalex_id и Short description для 9 статей (1 — GitHub репозиторий без статьи в OpenAlex). Дублирующаяся запись удалена.
- **Результат:** frame_sampling.md обновлён, все статьи с arXiv/CVPR имеют openalex_id и краткое описание.
- **Точка проверки:** `cat frame_sampling.md`

## 2026-10-17

**Запрос:** Найти 5 статей, ускоряющих модели (VLM / VideoLLM для video QA).

**Действие:** Поиск в OpenAlex по запросам: KV cache compression для VLM, token pruning для vision transformers, ускорение inference для VideoLLM.

**Результат:** Найдено 5 релевантных статей, записано в `library/model_acceleration_vlm.md`:
1. **VL-Cache** (2024) — KV cache compression с layer-adaptive sparsity, 2.33x speedup
2. **VisCache** (2026) — plug-and-play visual KV pruning, 2.35x speedup
3. **Feather the Throttle** (2025, ICCV) — multistage token pruning, исправление bias early pruning
4. **VidCom²** (2025, EMNLP) — frame-level adaptive compression для VideoLLM, 70.8% latency reduction
5. **VETO** (2026) — dual-axis (spatial + temporal) token optimization, 45% faster inference

**Точка проверки:** `library/model_acceleration_vlm.md`
**Итог:** ✓ Статьи найдены и записаны. Все методы — training-free / plug-and-play, применимы к qwen3-vl.


## 2026-10-18 — запуск baseline, DART и FastV в Kaggle

- Запрос: запустить три эксперимента для `baseline`, `dart` и `fastv` с `ratio=0.75`, `limit=0.05`, `fps=10`, `max_num_frames=16`, задачей `mvbench_action_count`, `dtype=float16` и `num_gpus=2`; не ждать завершения и залогировать запуски.
- Что сделано: актуальная версия notebook `ekaterinagrishina/testing` синхронизирована и без локальных правок отправлена в Kaggle как version 11; для каждого метода создан отдельный каталог в `results/` с `experiment.yaml`, `method.yaml` и `runner.yaml`.
- Результат: Kaggle принял kernel version 11, содержащую три последовательных запуска; статус при единственной проверке — `KernelWorkerStatus.QUEUED`. CSV и сущности Measurement не создавались, поскольку вычисления ещё не завершены.
- Точка проверки: `kaggle kernels status ekaterinagrishina/testing`; каталоги `results/*_r0.75_mvbench_action_count_2026-10-18_kaggle_v11/`.
- Итог проверки: удалённый `main` в момент запуска соответствовал commit `c5f8d71cdfb367c69dd2e45bc7fd9122d7090d38`; параметры трёх команд сверены с notebook; ожидание завершения и скачивание метрик намеренно не выполнялись.

