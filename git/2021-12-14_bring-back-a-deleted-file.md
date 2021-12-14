# Bring back a deleted file

When you're in a branch, and deleted a file, say from the main branch, and want to bring it back:

```
git restore --source main path/to/the/file/that/exists/on/main/but/not/the/current/branch
```

TADA! The file is back, no copy and paste or whatever
