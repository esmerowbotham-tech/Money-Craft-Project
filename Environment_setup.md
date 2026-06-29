# Environment Setup (conda)

Everyone gets identical packages from one file: `environment.yml`. Put it in the project folder first.

## If you don't have conda yet

Install **Miniforge** from <https://conda-forge.org/download/> (free, lightweight).
On Windows, use the **Miniforge Prompt** from the Start menu afterwards.

## Create the environment (everyone)

From the project folder (where `environment.yml` is):

```bash
conda env create -f environment.yml
conda activate moneycraft
```

## Register the kernel + launch JupyterLab

```bash
python -m ipykernel install --user --name moneycraft --display-name "Python (moneycraft)"
jupyter lab
```

Pick the **Python (moneycraft)** kernel in your notebooks.

## Everyday use

- Activate: `conda activate moneycraft`
- Deactivate: `conda deactivate`

## Adding a package later

Add it under `dependencies:` in `environment.yml`, commit it, then everyone runs:

```bash
conda env update -f environment.yml --prune
```