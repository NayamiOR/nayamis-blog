# 学习编程的五要素

_本文总结于 Michael Ryan Clarkson 的 OCaml Programming 课程。_

_解释部分有 Claude 大量参与。_

## 五要素

### 原文

1. Syntax: How do you write language constructs?
2. Semantics: What do programs mean? (Type checking evaluation rules)
3. ldioms: What are typical patterns for using language features to express your computation?
4. Libraries: What facilities does the language (or a third-party project) provides "standard"? (E.g, file access, data structures)
5. Tools: What do language implementations provide to make your job easier? (E.g, top-level, debugger, GUl editor, ...)

### 译文

1. 语法：如何编写语言结构？
2. 语义：程序的含义是什么？（类型检查评估规则）
3. 习语：使用语言功能来表达计算的典型模式是什么？
4. 库：语言（或第三方项目）提供的“标准”设施是什么？ （例如，文件访问，数据结构）
5. 工具：语言实现提供了什么来使您的工作更轻松？ （例如，顶级，调试器，GUI 编辑器，...）

### 说明

#### 语法

语法是一种规则，用于描述如何编写语言结构。比如语言中的所有关键字、符号、标识符的使用规则。语法掌握程度能决定写出的程序能不能通过编译，也就是正确掌握程序的编写方法。

#### 语义

语义指的是你的程序的逻辑，换句话说是你的算法设计，和代码组织设计，掌握代码的深层含义。除此之外包含了一些隐含的高级语法内容，是否能掌握这些也是语义重要的一环。

#### 习语

习语就是在程序、实际应用中代码中常用的解决方案。最经典的习语的解释就是设计模式。

编程语言的习语 (Idiom), 是指在使用该语言编程过程中形成的惯用代码组织结构或实现模式。

这些代码结构反映了语言开发者对特定问题通用解决方案的最佳实践（也就是"代码怎么写最好"的参考答案）。

使用这些习语可以更好地发挥语言的优势, 编写出更加地道和高效的代码。

举几个例子:

1. Python 中使用的 List Comprehension (列表推导式)是 Python 的重要习语, 可以简洁地处理列表数据。
2. Rust 中基于 Enum 和 Match 语句的自定义数据类型表示, 是 Rust 开发的重要习语。
3. Go 语言倾向使用 Struct 组合和 Interface 实现来达到面向对象编程的目的, 这也是 Go 语言的重要习语。
4. 面向对象编程中的各种设计模式, 例如工厂模式、单例模式等也是重要的面向对象习语。

总之, 编程语言的习语体现了语言最佳实践和编程思维模式。

#### 库

库一般是别人写好的代码库，可以在自己的代码中引用，以达到复用的目的，帮助我们少写代码。

比如在 Python 中我们经常使用第三方库。如 `numpy`、`pandas` 等，这些库都是别人写好的，我们可以直接引用，帮助我们少写代码。

很少有人放着这些库不用，一是为了省事、二是因为大家都用、三是因为自己写同样的代码大概率不如这些库写的好。

#### 工具

工具指我们写代码的时候用到的代码编辑和调试工具等。比如编辑器、编译器、调试器等。

一个符合习惯的工具可以增加效率，提高开发体验。
