## 事件

xorm支持两种方式的事件，一种是在Struct中的特定方法来作为事件的方法，一种是在执行语句的过程中执行事件。

在Struct中作为成员方法的事件如下：

* BeforeInsert()

在将此struct插入到数据库之前执行

* BeforeUpdate()

在将此struct更新到数据库之前执行

* BeforeDelete()

在将此struct对应的条件数据从数据库删除之前执行

* `func BeforeSet(name string, cell xorm.Cell)`

在 Get 或 Find 方法中，当数据已经从数据库查询出来，而在设置到结构体之前调用，name为数据库字段名称，cell为数据库中的字段值。

* `func AfterSet(name string, cell xorm.Cell)`

在 Get 或 Find 方法中，当数据已经从数据库查询出来，而在设置到结构体之后调用，name为数据库字段名称，cell为数据库中的字段值。

* AfterInsert()

在将此struct成功插入到数据库之后执行

* AfterUpdate()

在将此struct成功更新到数据库之后执行

* AfterDelete()

在将此struct对应的条件数据成功从数据库删除之后执行


在语句执行过程中的事件方法为：

* Before(beforeFunc interface{})

临时执行某个方法之前执行

```Go
before := func(bean interface{}){
    fmt.Println("before", bean)
}
engine.Before(before).Insert(&obj)
```

* After(afterFunc interface{})

临时执行某个方法之后执行

```Go
after := func(bean interface{}){
    fmt.Println("after", bean)
}
engine.After(after).Insert(&obj)
```

其中beforeFunc和afterFunc的原型为func(bean interface{}).
