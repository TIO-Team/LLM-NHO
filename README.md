https://ieeexplore.ieee.org/abstract/document/11509330

# LLM-NHO Solver (TSP & CVRP)

This folder contains our paper code for solving **TSP** and **CVRP** using **EOH-SIT** parameter heuristics:

- `eoh` (Evolution of Heuristics) generates two parameterized heuristics (JSON) via an LLM + evolutionary search.
- `SIL_test_eoh` runs experiments with the generated heuristics and reports results for **TSP** and **CVRP**.

> Note: This repository also includes the upstream EoH platform under `eoh/`.

## Project Layout

- `TSP/` TSP model + test scripts
- `CVRP/` CVRP model + test scripts
- `utils/` shared utilities

## Dependencies

This sub-project uses PyTorch for the neural solver plus common scientific packages. The original dependency list used in our experiments:

```bash
Python=3.8.6
matplotlib==3.5.2
numpy==1.23.3
pandas==1.5.1
pytz==2022.1
torch==1.12.1
torchaudio==0.12.1
torchvision==0.13.1
tqdm==4.64.1
```

## Data Download

The datasets and pretrained models used in our experiments can be downloaded from Baidu Cloud:

Baidu Netdisk:
https://pan.baidu.com/s/1-EEpgHWUh_cTooC8KIN6Qw
Extraction code: id75

## Quick Start (Reproduce Paper Results)

All commands below assume you are at the repository root `EoH-main/EoH-main/` (i.e., the directory that contains `SIL_test_eoh/` and `eoh/`).

### 1) Generate heuristics with EoH

This launches EoH to generate the two parameter heuristics (stored as JSON in the test folders):

```bash
cd eoh/src
PYTHONPATH=. python eoh/test/run.py
```

Before running, you must configure your LLM endpoint/key/model in `eoh/src/eoh/test/run.py`.

### 2) Run TSP experiments

```bash
cd SIL_test_eoh
PYTHONPATH=. python TSP/Test_All/test_old_set_heu.py
```

Outputs:

- TSP results are saved under `SIL_test_eoh/TSP/Test_All/results_2opt/<timestamp>/` as JSON files.

### 3) Run CVRP experiments

```bash
cd SIL_test_eoh
PYTHONPATH=. python CVRP/Test_All/test_old_set_heu.py
```

Outputs:

- CVRP results are saved under `SIL_test_eoh/CVRP/Test_All/results_2opt/<timestamp>/` as JSON files.

## Notes

- GPU: the scripts default to CUDA (`USE_CUDA = True`) and pick a GPU via `CUDA_DEVICE_NUM` inside the test scripts.
- Paths: the test scripts `chdir` to their own directory; run them from `SIL_test_eoh/` to keep relative paths consistent.

## Citation

If you use this code in your research, please cite our paper.

## Acknowledgements

This codebase builds on the public EoH platform and prior NCO implementations (e.g., SIL-style components). We thank the authors for open-sourcing their work.


## Important Notice

This repository contains the early research release used during our paper experiments. The primary goal of this version is to provide access to the core algorithms and experimental code rather than a production-ready software package.

As a result, users may encounter incomplete documentation, environment-specific configurations, hard-coded paths, or other deployment-related issues. Some setup and deployment details are intentionally left in their original research form and may require manual adjustment depending on your environment.

We plan to release a cleaner and more user-friendly version in the future, with improved documentation, code readability, dependency management, and deployment support.

Thank you for your patience and understanding.
