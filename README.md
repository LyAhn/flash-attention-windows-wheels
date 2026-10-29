# flash-attn 2.8.3.post1 - Windows wheel

Prebuilt `flash_attn-2.8.3.post1-cp312-cp312-win_amd64.whl`, available on the Releases page.

> **Compatibility warning:** this wheel only works with **Python 3.12**, **PyTorch 2.13.0+cu130** and **Windows x64**. The filename doesn't record the torch/CUDA version. In any other environment it will fail on import with a DLL error. It was built for sm_89 (RTX 40-series); other GPU architectures are untested.

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

## Verify

```
python -c "import flash_attn; print(flash_attn.__version__)"
python -c "import torch; from flash_attn import flash_attn_func; q=torch.randn(1,128,8,64,device='cuda',dtype=torch.float16); print(flash_attn_func(q,q,q,causal=True).shape)"
```

Both ran successfully on an RTX 4070 (sm_89) with the versions above.

## Attribution

FlashAttention is by Tri Dao and contributors: https://github.com/Dao-AILab/flash-attention. This repo only redistributes a Windows build, with a one-line-per-flag C++ standard patch, under the upstream BSD 3-Clause license (see `LICENSE`).
