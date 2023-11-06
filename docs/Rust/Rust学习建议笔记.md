笔记摘自以下视频：

[How to Learn Rust](https://www.youtube.com/watch?v=2hXNd6x9sZs&ab_channel=NoBoilerplate)

# 三大学习资料

1. Rust圣经
2. Rust by examples
3. Rustlings

三个资料相辅相成，建议搭配使用。

# 学习方法的建议

刷圣经，尽快从头到尾通读，如果遇到不理解的东西，记下来并继续。同时不要停止练习。

刷一遍圣经，然后开始做Rustlings的交互式练习。

Rustlings重在保持肌肉记忆，要保证对知识的肌肉记忆清晰且新鲜。

（第三步的支线：学习Haskell）

# 学习生命周期的建议

## 不用借用

用所有权，并分享所有事物

把变量输入进函数，如果之后还要用这个变量，那就把它返回回来，放弃所有权。

## 使用Copy和Clone

不要担心性能问题（毕竟Rust比Python快80倍）

## 遵从编译器

比如，在编译器没让你用引用的时候不要用引用。

这样最终会教你怎么合适地使用语法。