# Git

## Patch files

```bash
git diff > mypatch.patch
git apply mypatch.patch
```

`git diff` and `git apply` will work for text files, but won't work for binary files. But `git format-patch` does:

```bash
git format-patch <COMMIT>
git am <PATCH FILES>
```

Will give patch files for all commits from <COMMIT> upto the current branche's tip.

## Ipython Notebooks in Git

Put the following filter into the repo's config at `./.git/config`:

Install [jq](https://stedolan.github.io/jq/), if necessary.

```
[filter "nbstrip_full"]
        clean = "\"/d/Program Files/jq/jq\" --indent 1 \
                '(.cells[] | select(has(\"outputs\")) | .outputs) = []  \
                | (.cells[] | select(has(\"execution_count\")) | .execution_count) = null  \
                | .metadata = {\"language_info\": {\"name\": \"python\", \"pygments_lexer\": \"ipython3\"}} \
                | .cells[].metadata = {} \
                '"
        smudge = cat
        required = true
```

## Word with Git

Create `./.gitattributes` with:

```ini
*.docx diff=pandoc
```

Add to `./.git/config`:

```ini
[diff "pandoc"]
  textconv=pandoc --to=markdown
  prompt = false
[alias]
  wdiff = diff --word-diff=color --unified=1
```

See https://hrishioa.github.io/tracking-word-documents-with-git/

## Submodules

Submodules sind quasi Sub-Repos.

https://github.blog/2016-02-01-working-with-submodules/

Submodul zu einem Repo hinzufügen: `git submodule add <repository url> <new directory for submodule>`

Falls nötig, manuell Inhalte des Submoduls laden: `git submodule update --init --recursive`
Das hat Git früher nicht automatisch getan.

Ein Repo mit Submodulen klonen: `git clone --recursive <project url>`

Submodule eines, ohne --recursive geklonten, Repos laden: `git submodule update --init --recursive`

Submodules aus Quellen mit inoffiziellem SSL Zertifikat einbinden:
Die SSL Verifizierung muss für `git submodule add` in der globalen Konfiguration deaktiviert werden. Mit der lokalen Konfiguration reicht es nicht aus. Alternativ: Windows Zertifikatspeicher nutzen. (Eine Anleitung dafür ist hier auch zu finden.)

Submodul aktualisieren: Im Verzeichnis des Submoduls ganz normal Fetch, Pull, etc. machen und anschließend im übergeordneten Repo `git add [SUBREPO]` plus Commit. Oder `git submodule update --remote`.

## Unter der Haube / Technische Interna von Git

### Den Commit finden, der einen bestimmten Blob enthält

```sh
#!/bin/sh

git rev-list --all |
while read commit; do
    if git ls-tree -r $commit | grep -q "$1"; then
	    echo $(git log -n 1 $commit)
	    break
    fi
done
```

### Ort von Einstellungen

Um die Konfigurationsdatei herauszufinden, in der eine bestimmte Option enthalten ist: `git config --list --show-origin`

### Bash Titel anpassen (Git for Windows)

E.g. in `C:\Program Files\Git\etc\profile.d\git-prompt.sh`:

- Replace line `TITLEPREFIX=$MSYSTEM` with `TITLEPREFIX='git'`
- and `PS1='\[\033]0;$TITLEPREFIX:$PWD\007\]' # set window title` with

```
PS1='\[\033]0;$TITLEPREFIX:`basename $PWD`\007\]' # set window title
```
