# Installing the DualTalk environment (portable)

This repository includes a portable `environment.yml` that installs core conda packages and common pip-only Python packages. It intentionally excludes GPU/CUDA-specific packages (like CUDA-enabled `torch`) so the environment can be created on machines with different hardware.

Steps:

1. Create the environment from `environment.yml`:

```bash
conda env create -f environment.yml
```

2. Activate the environment:

```bash
conda activate dualtalk
```

3. Install PyTorch according to the target machine hardware.

- Example (CPU-only):

```bash
conda install -n dualtalk pytorch torchvision torchaudio cpuonly -c pytorch
```

- Example (CUDA on Linux) — visit https://pytorch.org/get-started/locally/ and follow the selector for your CUDA version, then run the printed `conda` command. Example:

```bash
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia
```

4. (Optional) If you need `pytorch3d` or other GPU-specific compiled packages install them after selecting the correct CUDA build for the target machine.

Notes:
- If any package in `environment.yml` fails to install, try adding `-c conda-forge` to the command or installing that package via `pip` inside the activated env.
- To reproduce an exact binary environment (less portable), consider using `conda env export --no-builds` or `conda-lock` to create lockfiles.

If you want, I can also:
- produce a `requirements.in` (direct pip deps) + pinned `requirements.txt` via `pip-compile`, or
- create `conda-lock` files for strict reproducibility.
