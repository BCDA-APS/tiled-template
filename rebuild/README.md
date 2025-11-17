# Rebuild the conda environment

The conda environment for this instance of MongoDB-backed tiled server
now needs to have specific package versions specified.  Here's the procedures:

## INSTALL

On the target workstation:

```bash
NEW_ENV=tiled-mongodb
conda env create -y -n "${NEW_ENV}" -f tiled-env.yml
conda activate "${NEW_ENV}"
grep -v file: pip-freeze.txt > pip-freeze-stripped.txt
python -m pip install -r pip-freeze-stripped.txt
```

## SOURCE

Use these steps to describe the conda environment that exists on the source
workstation:

```bash
conda activate conda_source_environment
python -m pip freeze --local > pip-freeze.txt
conda env export --no-builds > tiled-env.yml
```

In `tiled-env.yml`, comment out any pip installs from github, ...

> If you need fully self-contained relocatable envs, consider
> conda-pack (pack on source, unpack on target) which preserves
> pip installs as-is.
