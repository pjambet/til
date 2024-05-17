# Rebase a stack of commits without dealing with conflicts


```
git rebase --keep-base -i main
```

Docs: https://git-scm.com/docs/git-rebase#Documentation/git-rebase.txt---keep-base

Instead of checking the number of commits and then doing, assuming 3:

```
git rebase -i HEAD~3
```
