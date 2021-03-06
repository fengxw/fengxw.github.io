---
title:  Regex Basic
author: fengxw
tag: [regex, php]
---

This regex base on php syntax

---

## 常用正则函数

- preg_match //常用于表达验证
- preg_match_all
- preg_replace //常用于过滤非法词汇
- preg_filter
- preg_grep
- preg_quote

## 基本语法

### 界定符
$pattarn = “/[0-9]/“ //两个“/ /”，”# #”, “{ }” 大括号也是运算符，避免歧义一般不用

**`Tips: 正则表达式工具 regexpal`**

### 原子
最小匹配单位，unicode 编码表中的字符，包括可见符号和不可以见符号

**`Tips: 文字匹配（中文，日文等）先转换成 unicode 编码`**

### 元字符

#### 原子的筛选方式
- | 匹配两个或者多个分支选择
- \[ ] 匹配方括号中的任意一个原子
- \[^] 匹配除方括号中的原子之外的任意字符

#### 原子的集合
- . 匹配除换行符之外的任意字符
- \d 匹配任意一个十进制数字，即[0-9]
- \D 匹配任意一个非十进制数字，即[^0-9]
- \s 匹配一个不可见原子，即[\f\n\r\t\v]
- \S 匹配一个可见原子，即[^\f\n\r\t\v]
- \w 匹配任意一个数字、字母或下划线，即[0-9a-zA-Z]
- \W 匹配任意一个非数字、字母或下划线，即[^0-9a-zA-Z]

#### 量词
- {n} 表示其前面的原子恰好出现n次
- {n,} 表示其前面的原子最少出现n次
- {n,m} 表示其前面的原子最少出现n次，最多出现m次
- \* 匹配0次、1次或者多次其之前的原子，即{0,}
- \+ 匹配1次或者多次其之前的原子，即{1,}
- ? 匹配0次或者1次其之前的原子，即{0,1}

#### 边界控制和模式单元
- ^ 匹配字符串开始的位置
- $ 匹配字符串结尾的位置
- ( ) 匹配其中的整体位一个原子

## 高级应用
- 修正模式 '/im.+123/U’
- 在界定符末尾加 修正符 U，常见的修正符有一下几种：

    - U - 懒惰匹配 //匹配所有结果中长度最小的
    - i - 忽略英文字母大小写
    - x - 忽略空白 //包括空格、制表符、回车等产生的空白
    - s - 让元字符‘.’匹配包括换行符在内的所有字符

## 应用实例
- 非空 .+
- 浮点数 \d.\d{2}$ //保留两位小数的浮点数
- 手机号 1(3|4|5|7|8){9} or 1[34578]{9}
- email ^\w+(.\w)*@\w+(.\w)+$
- url ^(https?://)?(\w+.)[a-zA-Z]+$

