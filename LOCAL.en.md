# Local context of this llama.cpp clone

Russian base: [LOCAL.ru.md](LOCAL.ru.md).

Upstream: `https://github.com/ggml-org/llama.cpp`.
Pinned commit: `3cf03257f219afbe7334045ff7c6a06ac68c627d` ("CUDA: enable sparse fa for qwen4"),
branch `bench-3060ti` created exactly from it, MIT.

## Role in the project

- it provides the `ggml` subdirectory used to build the Strata engine (`-DSTRATA_GGML_DIR=…\llama.cpp`);
- it hosts a separate `llama-server` build (the server used for comparisons and MTP profiles).

The `llama-server.exe` the wrapper scripts actually use is built from the **vendored** snapshot
`..\engine\third_party\llama.cpp` (same commit, no `.git`). These are not two repositories but two
roles; both copies stay.

## Building llama-server

```bat
cmake -S . -B build -G Ninja -DGGML_CUDA=ON -DCMAKE_BUILD_TYPE=Release ^
  -DCMAKE_CUDA_ARCHITECTURES=86 -DCMAKE_CUDA_COMPILER=F:\CUDA\cuda-13.3\bin\nvcc.exe
cmake --build build --target llama-server -j 4
```

MTP flag check: `build\bin\llama-server.exe --help | findstr "spec-type"`.

## Reports of this machine

`bench-3060ti/` holds the measurement reports for the RTX 3060 Ti 8 GiB rig, in EN/RU pairs:
[llama-fork-report.md](bench-3060ti/llama-fork-report.md) (this fork),
[full-measurement-report.md](bench-3060ti/full-measurement-report.md) (both forks).
