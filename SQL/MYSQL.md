在 MySQL 中，`DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP` 是一种用于 `TIMESTAMP` 或 `DATETIME` 列的定义方式，它指定了两个功能：

1. **`DEFAULT CURRENT_TIMESTAMP`**:
    - 当插入一条新记录时，如果没有显式为这个列提供值，它会自动使用当前的时间戳作为默认值。
2. **`ON UPDATE CURRENT_TIMESTAMP`**:
    - 当更新这条记录时，每当发生更新操作时，这个列会自动更新为当前的时间戳。
```sql
CREATE TABLE example (
    id INT AUTO_INCREMENT PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
    );
```