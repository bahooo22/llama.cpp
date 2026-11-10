# Локальный контекст клона llama.cpp

Английский зеркал: [LOCAL.en.md](LOCAL.en.md).

Upstream: `https://github.com/ggml-org/llama.cpp`.
Зафиксированный коммит: `3cf03257f219afbe7334045ff7c6a06ac68c627d` («CUDA: enable sparse fa for
qwen4»), ветка `bench-3060ti` создана ровно от него, MIT.

## Роль в проекте

- поставщик подкаталога `ggml` для сборки движка Strata (`-DSTRATA_GGML_DIR=…\llama.cpp`);
- площадка для отдельной сборки `llama-server` (сервер для сравнений и MTP-профилей).

Рабочий `llama-server.exe`, которым пользуются скрипты обвязки, собран из **vendored** снимка
`..\engine\third_party\llama.cpp` (тот же коммит, без `.git`). Это не дубль-репозиторий, а две
роли; обе копии остаются.

## Сборка llama-server

```bat
cmake -S . -B build -G Ninja -DGGML_CUDA=ON -DCMAKE_BUILD_TYPE=Release ^
  -DCMAKE_CUDA_ARCHITECTURES=86 -DCMAKE_CUDA_COMPILER=F:\CUDA\cuda-13.3\bin\nvcc.exe
cmake --build build --target llama-server -j 4
```

Проверка MTP-флагов: `build\bin\llama-server.exe --help | findstr "spec-type"`.

## Отчёты по этому стенду

В `bench-3060ti/` лежат отчёты по замерам на RTX 3060 Ti 8 ГиБ, парами EN/RU:
[llama-fork-report.ru.md](bench-3060ti/llama-fork-report.ru.md) (этот форк),
[full-measurement-report.ru.md](bench-3060ti/full-measurement-report.ru.md) (оба форка).
