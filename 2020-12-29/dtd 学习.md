---
title: dtd 学习
date: 2020-12-29 11:04:38
tags:
---

### dtd 学习

参考:[菜鸟教程](https://www.runoob.com/dtd/dtd-intro.html)

#### 元素属性类型

- 几个特殊类型
  - CDATA 字符数据,不会去尝试解析该字符数据中有没有标记或实体,简单理解就是普通文本类型
  - PCDATA 被解析的字符数据,xml解析器会去解析该文本,

- 实体

  说明:实体是用于定义普通文本或特殊字符的快捷方式的变量

  特点: 实体引用是对实体的引用; 实体可在内部或外部进行声明

  构成:一个实体由3部分构成:一个'&'号,一个名称,一个';' 分号

   在html 中常见的&nbsp; 标识一个空格,就是一个实体

  实体如下:

  | 实体引用 | 字符 |
  | -------- | ---- |
  | &lt;     | <    |
  | &gt;     | >    |
  | &amp;    | &    |
  | &quot;   | "    |
  | &apos;   | '    |

  

  ####  一个简单的例子

  ```
  <!DOCTYPE root-element [element-declarations]> 
  ```

  这里定义了 root-element xml文档根元素的名称

  #### 声明一个元素

  在 DTD 中，XML 元素通过元素声明来进行声明。元素声明使用下面的语法：

  ```
  <!ELEMENT element-name category>
   或
   <!ELEMENT element-name (element-content)>
  ```

  可以直接在 元素名称 element-name 后面指定 元素的属性

  也可以用 括号,指定元素的具体内容

  ##### 空元素

  ```
  <!ELEMENT element-name EMPTY>
  ```

  ##### 带任何内容的元素

  ```
  <!ELEMENT element-name ANY>
  ```

  ##### 带有子元素（序列）的元素

  ```
  <!ELEMENT element-name (child1,child2,...)>
  ```

  当子元素按照由逗号分隔开的序列进行声明时，这些子元素必须按照相同的顺序出现在文档中。在一个完整的声明中，子元素也必须被声明，同时子元素也可拥有子元素

  ##### 声明只出现一次的元素

  ```
  <!ELEMENT element-name (child-name)>
  ```

  ##### 声明最少出现一次的元素

  ```
  <!ELEMENT element-name (child-name+)>
  ```

  ##### 声明出现零次或多次的元素

  ```
  <!ELEMENT element-name (child-name*)>
  ```

  ##### 声明出现零次或一次的元素

  ```
  <!ELEMENT element-name (child-name?)>
  ```

  ##### 声明"非.../即..."类型的内容

  ```
  <!ELEMENT note (to,from,header,(message|body))> 
  ```

  上面的例子声明了："note" 元素必须包含 "to" 元素、"from" 元素、"header" 元素，以及非 "message" 元素即 "body" 元素。

  ##### 声明混合型的内容

  ```
  <!ELEMENT note (#PCDATA|to|from|header|message)*> 
  ```

  上面的例子声明了："note" 元素可包含出现零次或多次的 PCDATA、"to"、"from"、"header" 或者 "message"。

  #### 声明属性

  在 DTD 中，属性通过 ATTLIST 声明来进行声明。

  ```
  <!ATTLIST element-name attribute-name attribute-type attribute-value>
  ```

  ##### 属性类型选项

  | 类型               | 描述                          |
  | ------------------ | ----------------------------- |
  | CDATA              | 值为字符数据 (character data) |
  | (*en1*\|*en2*\|..) | 此值是枚举列表中的一个值      |
  | ID                 | 值为唯一的 id                 |
  | IDREF              | 值为另外一个元素的 id         |
  | IDREFS             | 值为其他 id 的列表            |
  | NMTOKEN            | 值为合法的 XML 名称           |
  | NMTOKENS           | 值为合法的 XML 名称的列表     |
  | ENTITY             | 值是一个实体                  |
  | ENTITIES           | 值是一个实体列表              |
  | NOTATION           | 此值是符号的名称              |
  | xml:               | 值是一个预定义的 XML 值       |

  ##### 默认**属性值**可使用下列值 :

  | 值           | 解释           |
  | ------------ | -------------- |
  | 值           | 属性的默认值   |
  | #REQUIRED    | 属性值是必需的 |
  | #IMPLIED     | 属性不是必需的 |
  | #FIXED value | 属性值是固定的 |