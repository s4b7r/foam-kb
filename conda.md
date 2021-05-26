# conda

### Conda selbst aktualisieren

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

## Spezifische Paket Version / Build installieren

```bat
conda install PAKET=VERSION
```

```bat
conda install PAKET=VERSION=BUILD
```


## Conda Environment Revisions / History

### Revisions anzeigen

```bat
conda list --revisions
```

### Revision wiederherstellen

```bat
conda install --revision NUMBER
```
