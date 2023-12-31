
Rust 中有两个常见的 trait，Clone 和 Copy，许多初学者没有搞明白。今天我们来专门谈一谈这两个 trait。

## Copy 的含义

Copy 的全名是 std::marker:: Copy。请大家注意 std:: marker 这个模块里面的所有的 trait 都是特殊的 trait。目前稳定的有四个，它们是 Copy、Send、Sized、Sync。它们的特殊之处在于它们是跟编译器密切绑定的，impl 这些 trait 对编译器的行为有重要影响。在编译器眼里，它们与其它的 trait 不一样。这几个 trait 内部都没有方法，它们的唯一任务是，给类型打一个“标记”，表明它符合某种约定，这些约定会影响编译器的静态检查以及代码生成。

Copy 这个 trait 在编译器的眼里代表的是什么意思呢？简单点总结就是说，如果一个类型 impl 了 Copy trait，意味着任何时候，我们可以通过简单的内存拷贝 (C 语言的按位拷贝 memcpy)实现该类型的复制，而不会产生任何问题。

一旦一个类型实现了 Copy trait，那么它在变量绑定、函数参数传递、函数返回值传递等场景下，它都是 copy 语义，而不再是默认的 move 语义。

## Copy 的实现条件

并不是所有的类型都可以实现 Copy trait。Rust 规定，对于自定义类型，只有所有的成员都实现了 Copy trait，这个类型才有资格实现 Copy trait。

常见的数字类型、bool 类型、共享借用指针&，都是具有 Copy 属性的类型。而 Box、Vec、可写借用指针&mut 等类型都是不具备 Copy 属性的类型。

对于数组类型，如果它内部的元素类型是 Copy，那么这个数组也是 Copy 类型。

对于 tuple 类型，如果它的每一个元素都是 Copy 类型，那么这个 tuple 会自动实现 Copy trait。

对于 struct 和 enum 类型，不会自动实现 Copy trait。而且只有当 struct 和 enum 内部每个元素都是 Copy 类型的时候，编译器才允许我们针对此类型实现 Copy trait。

我们可以认为，Rust 中只有 [POD](https://link.zhihu.com/?target=https%3A//en.wikipedia.org/wiki/Passive_data_structure) (C++语言中的 Plain Old Data) 类型才有资格实现 Copy trait。在 Rust 中，如果一个类型只包含 POD 数据类型的成员，没有指针类型的成员，并且没有自定义析构函数（实现 Drop trait），那它就是 POD 类型。比如整数、浮点数、只包含 POD 类型的数组等，都属于 POD 类型。而 Box、 String、 Vec 等，不能按 bit 位拷贝的类型，都不属于 POD 类型。但是，反过来讲，并不是所有的 POD 类型都应该实现 Copy trait。

## Clone 的含义

Clone 的全名是 std::clone:: Clone。它的完整声明是这样的：

```rust
pub trait Clone : Sized {
    fn clone(&self) -> Self;
    fn clone_from(&mut self, source: &Self) {
        *self = source.clone()
    }
}

```

它有两个关联方法，其中 clone_from 是有默认实现的，它依赖于 clone 方法的实现。clone 方法没有默认实现，需要我们手动实现。

clone 方法一般用于“基于语义的复制”操作。所以，它做什么事情，跟具体类型的作用息息相关。比如对于 Box 类型，clone 就是执行的“深拷贝”，而对于 Rc 类型，clone 做的事情就是把引用计数值加 1。

虽然说，Rust 中 clone 方法一般是用来执行复制操作的，但是你如果在自定义的 clone 函数中做点什么别的工作编译器也没法禁止，你可以根据情况在 clone 函数中编写任意的逻辑。但是有一条规则需要注意：对于实现了 Copy 的类型，它的 clone 方法应该跟 Copy 语义相容，等同于按位拷贝。

## 自动 derive

绝大多数情况下，实现 Copy Clone 这样的 trait 都是一个重复而无聊的工作。因此，Rust 提供了一个 attribute，让我们可以利用编译器自动生成这部分代码。示例如下：

```
#[derive(Copy, Clone)]
struct MyStruct(i32);

```

这里的 derive 会让编译器帮我们自动生成 impl Copy 和 impl Clone 这样的代码。自动生成的 clone 方法，就是依次调用每个成员的 clone 方法。

通过 derive 方式自动实现 Copy 和手工实现 Copy 有一丁点的微小区别。当类型具有泛型参数的时候，比如 struct MyStruct<T>{}，通过 derive 自动生成的代码会自动添加一个 T: Copy 的约束。

目前，只有一部分固定的特殊 trait 可以通过 derive 来自动实现。将来 Rust 会允许自定义的 derive 行为，让我们自己的 trait 也可以通过 derive 的方式自动实现。

## 总结

Copy 和 Clone 两者的区别和联系有：

1. Copy 内部没有方法，Clone 内部有两个方法。
2. Copy trait 是给编译器用的，告诉编译器这个类型默认采用 copy 语义，而不是 move 语义。Clone trait 是给程序员用的，我们必须手动调用 clone 方法，它才能发挥作用。
3. Copy trait 不是你想实现就实现，它对类型是有要求的，有些类型就不可能 impl Copy。Clone trait 没有什么前提条件，任何类型都可以实现（unsized 类型除外）。
4. Copy trait 规定了这个类型在执行变量绑定、函数参数传递、函数返回等场景下的操作方式。即这个类型在这种场景下，必然执行的是“简单内存拷贝”操作，这是由编译器保证的，程序员无法控制。Clone trait 里面的 clone 方法究竟会执行什么操作，则是取决于程序员自己写的逻辑。一般情况下，clone 方法应该执行一个“深拷贝”操作，但这不是强制的，如果你愿意，也可以在里面启动一个人工智能程序，都是有可能的。
5. 如果你确实需要 Clone trait 执行“深拷贝”操作，编译器帮我们提供了一个工具，我们可以在一个类型上添加#[derive (Clone)]，来让编译器帮我们自动生成那些重复的代码。
6. 然而 Rust 语言规定了当 T: Copy 的情况下，Clone trait 代表的含义。即：当某变量`let t: T`;，符合`T: Copy`时，它调用 `let x = t.clone ()` 方法的时候，它的含义必须等同于“简单内存拷贝”。也就是说，clone 的行为必须等同于`let x = std::ptr:: read (&t)`;，也等同于`let x = t`;。当 T: Copy 时，我们不要在 Clone trait 里面乱写自己的逻辑。所以，当我们需要指定一个类型是 Copy 的时候，最好顺便也指定它 Clone 的行为，就是编译器为我们自动生成的那个逻辑。正因为如此，在希望让一个类型具有 Copy 性质的时候，一般使用 `#[derive (Copy, Clone)]` 这种方式，这种情况下它们俩最好一起出现，避免手工实现 Clone 导致错误。

​

本文同步发布在微信公众号：**Rust 编程**，欢迎关注。