## 执行SQL查询

### Query

也可以直接执行一个SQL查询，即Select命令。在Postgres中支持原始SQL语句中使用 ` 和 ? 符号。

```Go
sql := "select * from userinfo"
results, err := engine.Query(sql)
```

当调用 `Query` 时，第一个返回值 `results` 为 `[]map[string][]byte` 的形式。

`Query` 的参数也允许传入 `*builder.Buidler` 对象

```Go
// SELECT * FROM table
results, err := engine.Query(builder.Select("*").From("table"))
```

### QueryInterface

和 `Query` 类似，但是返回值为 `[]map[string]interface{}`

### QueryString

和 `Query` 类似，但是返回值为 `[]map[string]string`