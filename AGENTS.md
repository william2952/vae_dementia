# AGENTS.md

## Cursor Cloud specific instructions

### Project Overview

Research ML project for dementia classification using FDG-PET brain imaging with a Variational Autoencoder (VAE) + Graph Convolutional Network (GCN). All code lives in Jupyter notebooks under `vae_files/`. See `README.md` for notebook descriptions.

### Environment

- Python 3.12 virtual environment at `.venv/` (project specifies 3.11 in `environment.yml`, but all pinned dependencies install and work correctly on 3.12).
- Activate with: `source /workspace/.venv/bin/activate`

### Key Gotchas

- **`svlite` is not on PyPI.** It must be installed from GitHub: `pip install git+https://github.com/Neurology-AI-Program/svlite.git`. The `requirements.txt` entry `svlite==1.0.0` will fail; install separately.
- **`svlite` import paths differ** between the installed package and what `latent_space.ipynb` uses. The notebook imports `from svlite.svlite.data_structures import ...` but the pip-installed package uses `from svlite.data_structures import ...`.
- **Data files are gitignored.** All notebooks require data in `vae_files/model_data/` (CSV, Parquet, NIfTI, `.pt` model weights). These must be obtained separately — notebooks cannot run end-to-end without them.
- **No GPU required.** Code falls back to CPU when neither CUDA nor MPS is available. Training is slower but functional.

### Running Services

- **Jupyter Lab:** `source /workspace/.venv/bin/activate && jupyter lab --no-browser --port=8888 --ip=0.0.0.0 --NotebookApp.token='' --allow-root`

### Linting

- `source /workspace/.venv/bin/activate && nbqa flake8 vae_files/ --max-line-length=120`

### Testing

No automated test suite exists. Validation is done by running notebook cells and inspecting outputs (loss curves, model summaries, visualizations). The VAE architecture can be tested with synthetic data without the real dataset.
