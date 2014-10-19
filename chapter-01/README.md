## 创建Orm引擎

在xorm里面，可以同时存在多个Orm引擎，一个Orm引擎称为Engine。因此在使用前必须调用`xorm.NewEngine`，如：

```Go
import (
    _ "github.com/go-sql-driver/mysql"
    "github.com/go-xorm/xorm"
)
engine, err := xorm.NewEngine("mysql", "root:123@/test?charset=utf8")
defer engine.Close()
```

or

```Go
import (
    _ "github.com/mattn/go-sqlite3"
    "github.com/go-xorm/xorm"
    )
engine, err = xorm.NewEngine("sqlite3", "./test.db")
defer engine.Close()
```

你可以创建一个或多个engine, 不过一般如果操作一个数据库，只需要创建一个Engine即可。每个Engine都支持在多GoRutine下使用。

xorm当前支持五种驱动四个数据库如下：

* Mysql: [github.com/Go-SQL-Driver/MySQL](https://github.com/Go-SQL-Driver/MySQL)

* MyMysql: [github.com/ziutek/mymysql](https://github.com/ziutek/mymysql)

* SQLite: [github.com/mattn/go-sqlite3](https://github.com/mattn/go-sqlite3)

* Postgres: [github.com/lib/pq](https://github.com/lib/pq)

* MsSql: [github.com/lunny/godbc](https://githubcom/lunny/godbc)

NewEngine传入的参数和`sql.Open`传入的参数完全相同，因此，使用哪个驱动前，请查看此驱动中关于传入参数的说明文档。

* [sqlite3](http://godoc.org/github.com/mattn/go-sqlite3#SQLiteDriver.Open)

* [mysql dsn](https://github.com/go-sql-driver/mysql#dsn-data-source-name)

* [mymysql](http://godoc.org/github.com/ziutek/mymysql/godrv#Driver.Open)

* [postgres](http://godoc.org/github.com/lib/pq)

在engine创建完成后可以进行一些设置，如：

1.错误显示设置，默认如下均为`false`

* `engine.ShowSQL = true`，则会在控制台打印出生成的SQL语句；
* `engine.ShowDebug = true`，则会在控制台打印调试信息；
* `engine.ShowError = true`，则会在控制台打印错误信息；
* `engine.ShowWarn = true`，则会在控制台打印警告信息；

2.如果希望用其它方式记录，则可以`engine.Logger`赋值为一个`io.Writer`的实现。比如记录到Log文件，则可以：

```Go
f, err := os.Create("sql.log")
    if err != nil {
        println(err.Error())
        return
    }
engine.Logger = xorm.NewSimpleLogger(f)
```

3.engine内部支持连接池接口。

* 如果需要设置连接池的空闲数大小，可以使用`engine.SetMaxIdleConns()`来实现。
* 如果需要设置最大打开连接数，则可以使用`engine.SetMaxOpenConns()`来实现。
