- Q: 我们在数据库操作的时候，比如 dao 层中当遇到一个 sql.ErrNoRows 的时候，是否应该 Wrap 这个 error，抛给上层。为什么，应该怎么做请写出代码？
- A: 应该
  - Dao只是数据对象的封装，并不负责处理真正的业务逻辑
  - ErrNoRows和具体的数据操作行为有关，比如insert成功的时候，并不返回任何row，这个时候的error并不是真正的字面意思的“error”，这些情况在Dao层是无法获取到应用的语义的
  - 代码：
    ```go
    return errors.Wrapf(code.NotFound, fmt.Sprintf("sql: %s error: %v", sql, err))
    ```
