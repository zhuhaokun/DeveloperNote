```sql
INSERT INTO users (id, name, email)
VALUES (1, 'John Doe', 'john.doe@example.com')
ON DUPLICATE KEY UPDATE name = VALUES(name), email = VALUES(email);
```
- 如果 `id` = 1 的记录不存在，这条语句会插入一条新记录。
- 如果 `id` = 1 的记录已存在，它会更新该记录的 `name` 和 `email` 字段为新提供的值。