# conda

## Conda selbst aktualisieren

```bat
conda update conda
```

## Initialize Conda prompt

Powershell: `conda init powershell`

## Conda Environments

### Conda Environment erstellen

```bat
conda create --name <NEW_ENV_NAME>
```

```bat
conda create --prefix <NEW_ENV_PATH>
```

### Conda Environment klonen

```bat
conda create --name <NEW_ENV_NAME> --clone <OLD_ENV_NAME>
```

### Conda Environment entfernen

```bat
conda remove --name myenv --all
```

### Conda Environment umbenennen

Geht leider nicht. Lösung: Klonen und altes entfernen.

### requirements.txt erstellen

```bat
conda list --export > requirements.txt
```

### Environments default Pfad ändern

`conda config --add envs_dirs c:\conda-envs`

`c:\users\[USER]\.condarc`

https://conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html#specify-environment-directories-envs-dirs

## Paketmanagemetn

### Install from requirements.txt

```bat
conda install --file requirements.txt
```

### Spezifische Paket Version / Build installieren

```bat
conda install PAKET=VERSION
```

```bat
conda install PAKET=VERSION=BUILD
```

https://docs.conda.io/projects/conda-build/en/latest/resources/package-spec.html#package-match-specifications

## Conda Environment Revisions / History

### Revisions anzeigen

```bat
conda list --revisions
```

### Revision wiederherstellen

```bat
conda install --revision NUMBER
```
