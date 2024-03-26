# The `cut` command 

Convenient command to trim each line, especially if they all share a common format. The following grabs all the values in the environemnts, splits on `.` and only selects the first two parts

```
env | grep -i <SOMETHING> | cut -d '.' -f 1,2
```
