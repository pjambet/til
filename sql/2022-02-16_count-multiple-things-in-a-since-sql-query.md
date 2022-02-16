# Count multiple things in a single sql query

Say that I want to count the rows in a table where a given column is null and not null,
after filtering. For instance a `users` table where users were created after a given
date and count the ones with a username, the ones without:

```sql
SELECT count(1) AS total,
    sum(case when username is null then 1 else 0 end) AS WithoutUsername,
    sum(case when username is not null then 1 else 0 end) AS WithUsername
FROM users
WHERE created_at >= ?
```

Source: https://stackoverflow.com/a/12789493
