json中不能有注释
```json
// comment
{
  "key": "value" // comment
}
```

解法：
使用字段key加前缀做注释key

例如加入属性的key是`xyz`, 则`?xyz`作为注释字段。这样的好处是，没有重名的字段，完全符合JSON协议。常用的前缀还有`#,` `_`, `__`等
```json
{
  "name": "Roman",
  "?name": "defines a nickname"
}
```