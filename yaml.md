- [1. introduction](#1-introduction)
- [2. 缩进](#2-缩进)
- [3. Key-Value pairs](#3-key-value-pairs)
- [4. list](#4-list)
- [5. 引用](#5-引用)
- [6. corresponding json](#6-corresponding-json)
# 1. introduction



YAML 的配置文件后缀为`.yml`，如：`hello.yml`

大小写敏感

`#`表示注释

# 2. 缩进
- 使用缩进表示层级关系
- 缩进不允许使用tab，只允许空格
- 缩进的空格数不重要，只要相同层级的元素左对齐即可
- there MUST be spaces between element parts.

# 3. Key-Value pairs
```yaml
key: value
```
notice: If there is not a space after colon Name:Value, it is wrong.

```yaml
key: {child-key: value1, child-key2: value2}

key: 
    child-key: value1
    child-key2: value2
```
```yaml
?  
    - complexkey1
    - complexkey2
:
    - complexvalue1
    - complexvalue2
```

examples:
```yaml
intNumber: 299
binaryNumber: 0b1010_0111_0100_1010_1110    #二进制表示

floatNumber1: 3.14
floatNumber2: 6.8523015e+5  #可以使用科学计数法

quotedText: "some text description"     # " or '
moreQuotedtext: strings do not have to be quoted, but I prefer to do it=
multipleText:
    - newline
      newline2    #字符串可以拆成多行，每一行会被转化成一个空格
we can also have spaces in keys: and also in values

# TRUE, true, True, FALSE, false, False 都可以
boolean: true

# 日期只能用两种格式
date: 2018-02-17    # ISO 8601格式，即yyyy-MM-dd
datetime: 2018-02-17T15:02:31+08:00    # ISO 8601格式，时间和日期之间使用T连接，最后使用+代表时区

nullKeyValue1: null
nullKeyValue2: 'node'
nullKeyValue3: ~ 
```
# 4. list

```yaml
key: [value1, value2]

key: 
 - value1
 - value2
```

# 5. 引用

`&` 用来建立锚点，`<<` 表示合并到当前数据，`*` 用来引用锚点。

```yaml
defaults: &defaults
  adapter:  postgres
  host:     localhost

development:
  database: myapp_development
  <<: *defaults

test:
  database: myapp_test
  <<: *defaults
```
相当于:

```yaml
defaults:
  adapter:  postgres
  host:     localhost

development:
  database: myapp_development
  adapter:  postgres
  host:     localhost

test:
  database: myapp_test
  adapter:  postgres
  host:     localhost
```

下面是另一个例子:

```yaml
list:
    - &showell Steve 
    - Clark 
    - Brian 
    - Oren 
    - *showell 
```
即

```yaml
list: ['Steve', 'Clark', 'Brian', 'Oren', 'Steve']
```

# 6. corresponding json
```yaml
languages:
  - Ruby
  - Perl
  - Python 
websites:
  YAML: yaml.org 
  Ruby: ruby-lang.org 
  Python: python.org 
  Perl: use.perl.org
```
转换为 json 为：
```json
{ 
  languages: [ 'Ruby', 'Perl', 'Python'],
  websites: {
    YAML: 'yaml.org',
    Ruby: 'ruby-lang.org',
    Python: 'python.org',
    Perl: 'use.perl.org' 
  } 
}
```
