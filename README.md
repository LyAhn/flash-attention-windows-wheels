# flash-attn 2.8.3.post1 - Windows wheel

Prebuilt `flash_attn-2.8.3.post1-cp312-cp312-win_amd64.whl`, available on the Releases page.

- Python 3.12, Windows 11 x64
- PyTorch 2.13.0+cu130, CUDA toolkit 13.0
- Built from upstream commit `a8aa52b1ab3e9ca574c8a33b3f35afc017ffa2e2` of Dao-AILab/flash-attention
- Built for and tested on an RTX 4070 (sm_89)

## Patch

`setup-c++20.patch` changes `-std=c++17` to `-std=c++20` in `setup.py`.

## Build

```
set DISTUTILS_USE_SDK=1
set MAX_JOBS=2
pip wheel . --no-build-isolation --no-deps -w dist
```

Run from an x64 VS developer prompt. Each `cicc` process uses roughly 2-4 GB of RAM, so keep other heavy jobs closed or the build can die with `LLVM ERROR: out of memory`.

## Install

```
pip install flash_attn-2.8.3.post1-cp312-cp312-win_amd64.whl
```
