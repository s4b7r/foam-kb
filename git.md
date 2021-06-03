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
