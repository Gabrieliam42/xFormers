# xFormers 0.0.33.post2 Windows Wheel

Prebuilt Windows wheel for xFormers, built from official upstream `facebookresearch/xformers`.

## Published Wheel

- Filename: `xformers-0.0.33.post2-1torch2.9.1cu130cuda13.2triton3.6.0.post26-cp39-abi3-win_amd64.whl`
- Package version: `xformers==0.0.33.post2`
- Python compatibility tag: `cp39-abi3-win_amd64`
- Build/test environment provenance: Python `3.12.10`
- Torch stack provenance: `torch==2.9.1+cu130`, `torchvision==0.24.1+cu130`, `torchaudio==2.9.1+cu130`
- CUDA toolkit used to build: `13.2`
- Triton runtime used during validation: `triton-windows==3.6.0.post26`
- GPU architecture used for build targeting: `8.0;8.6`
- Tested GPU: RTX 3090 (`sm_86`)
- Size: `2,543,938` bytes
- SHA256: `6d9cb42748e22ebbac785494920f2890424bd895d73cad5f735b68294b868dc7`

## Source

- Upstream repository: `https://github.com/facebookresearch/xformers`
- Upstream tag built: `v0.0.33.post2`

Note: upstream tag `v0.0.33.post2` currently has `version.txt` set to `0.0.34`, so the wheel build forced `BUILD_VERSION=0.0.33.post2` to keep the package version aligned with the requested tag.

## Verification

Validation was run from `D:\AI_Research`, not from the build workspace root.

Confirmed in `.venv312`:

- `xformers.__version__ == 0.0.33.post2`
- `torch.__version__ == 2.9.1+cu130`
- `torch.version.cuda == 13.0`
- `python -m xformers.info` reports:
  - `build.torch_version: 2.9.1+cu130`
  - `build.python_version: 3.12.10`
  - `build.cuda_version: 1302`
  - `build.nvcc_version: 13.2.51`
  - `build.env.TORCH_CUDA_ARCH_LIST: 8.0;8.6`
  - `is_triton_available: True`
  - `memory_efficient_attention.triton_splitKF: available`
  - `indexing.scaled_index_addF: available`
  - `indexing.scaled_index_addB: available`
  - `indexing.index_select: available`
- Triton-backed `index_select_cat` forward/backward succeeded on CUDA
- Triton-backed `scaled_index_add` forward/backward succeeded on CUDA
- `xformers.ops.memory_efficient_attention` forward/backward also succeeded on CUDA

Important distinctions:

- PyTorch reports runtime CUDA `13.0` because the installed stack is `cu130`
- xFormers itself was compiled with CUDA toolkit `13.2`, confirmed by `xformers.info`
- Triton support in this xFormers release is runtime-enabled by importing Triton
- The wheel metadata itself does not declare a Triton dependency

## Install

```powershell
python -m pip install torch==2.9.1+cu130 torchvision==0.24.1+cu130 torchaudio==2.9.1+cu130 --index-url https://download.pytorch.org/whl/cu130 --extra-index-url https://pypi.org/simple
python -m pip install triton-windows==3.6.0.post26
python -m pip install .\xformers-0.0.33.post2-1torch2.9.1cu130cuda13.2triton3.6.0.post26-cp39-abi3-win_amd64.whl
```

## Notes

- On this Windows stack, Triton-backed optimizations require `triton-windows`; there is no matching official `triton` package for this environment
- Without Triton installed, the wheel still imports and works, but Triton-backed operators stay unavailable
