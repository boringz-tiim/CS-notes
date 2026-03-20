#YAML学习笔记
## YAML概述
YAML(YAML Ain't Markup Language)是一种标记语言，其数据结构与JSON类似，但使用了YAML独有的缩进、标点符号等特性，使其更容易阅读和编写。

## YAML语法
### 基本语法
YAML的基本语法规则如下：

1. 大小写敏感
2. 使用缩进表示层级关系
3. 缩进只能用空格，不能使用制表符
4. 缩进的空格数目不重要，只要相同层级的元素左侧对齐即可
5. 句末加上“:”表示开始一个新节点
6. 句末加上“-”表示开始一个新列表元素
7. 多个连续的“-”表示一个空列表元素
8. 字符串用双引号或单引号表示
9. 布尔值用true或false表示
10. 整数和浮点数直接写出数字
11. 日期格式：YYYY-MM-DD HH:MM:SS
12. 数组和字典的开始和结束标记由“{}”和“[]”表示

### 示例
```yaml
# 基本数据类型
name: Tom
age: 25
married: true

# 数组
fruits:
  - apple
  - banana
  - orange

# 字典
person:
  name: John
  age: 30
  hobbies:
    - reading
    - swimming