# xFormers 0.0.33.post2 Windows Wheel

Prebuilt Windows wheel for xFormers, built from official upstream `facebookresearch/xformers`.

## Published Wheel

- Filename: `xformers-0.0.33.post2-1torch2.9.1cu130cuda13.2-cp39-abi3-win_amd64.whl`
- Package version: `xformers==0.0.33.post2`
- Python compatibility tag: `cp39-abi3-win_amd64`
- Build/test environment provenance: Python `3.12.10`
- Torch stack provenance: `torch==2.9.1+cu130`, `torchvision==0.24.1+cu130`, `torchaudio==2.9.1+cu130`
- CUDA toolkit used to build: `13.2`
- GPU architecture used for build targeting: `8.0;8.6`
- Tested GPU: RTX 3090 (`sm_86`)
- Size: `2,543,796` bytes
- SHA256: `dc0fc7b674b3714d3d77386840dbf383ba7e6ee2c7e6098af45e0f286dccd187`

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
- `xformers.ops.memory_efficient_attention` forward pass succeeded on CUDA
- backward pass succeeded on CUDA

Important distinction:

- PyTorch reports runtime CUDA `13.0` because the installed stack is `cu130`
- xFormers itself was compiled with CUDA toolkit `13.2`, confirmed by `xformers.info`

## Install

```powershell
python -m pip install torch==2.9.1+cu130 torchvision==0.24.1+cu130 torchaudio==2.9.1+cu130 --index-url https://download.pytorch.org/whl/cu130 --extra-index-url https://pypi.org/simple
python -m pip install .\xformers-0.0.33.post2-1torch2.9.1cu130cuda13.2-cp39-abi3-win_amd64.whl
```

## Notes

- Triton is not installed in the test environment, so Triton-backed optimizations are unavailable
- The wheel itself imports and runs correctly without Triton
