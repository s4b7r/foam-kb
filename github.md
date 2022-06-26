# github

## Mirror all my repos

Based on https://stackoverflow.com/a/68770988

```bash
gh repo list --limit 1000 | while read -r repo _; do
    echo $repo
    rep=`echo $repo | cut -d/ -f2`
    echo $rep
    gh repo clone "$repo" "GH_$rep" -- --mirror
done
```
