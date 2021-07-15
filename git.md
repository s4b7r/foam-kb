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

