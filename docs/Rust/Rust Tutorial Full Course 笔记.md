原视频链接

[Rust Tutorial Full Course](https://www.youtube.com/watch?v=ygL_xcavzQ4&t=8230s&ab_channel=DerekBanas)

目录

# 项目创建和管理

# 基础语法

## main函数

```go
fn main(){
	println!("Hello World");
}
```

`println!`是一个宏，用于输出

## 变量

声明变量，如果有`mut`则说明是可变变量，不然默认不可变。

```rust
let name=String::new();
let mut age=5;
let luckyNum :i32=8;
```

## 条件运算符

比如if表达式，在Rust中是表达式，而不只是语句。所以可以有一个返回值。

```rust
let number = 5;
let result = if number > 0 {
    "Positive"
} else {
    "Non-positive"
};
println!("{}", result);
```

## Match

有点像其它语言中的`Switch`。

```rust
fn main() {
    let number = 5;

    match number {
        0 => println!("Number is zero"),
        1 | 2 => println!("Number is one or two"),
        3..=5 => println!("Number is between three and five"),
        _ => println!("Number is something else"),
    }
}
```

# Array

```rust
fn main() {
    // 创建一个包含5个元素的整数数组
    let numbers: [i32; 5] = [1, 2, 3, 4, 5];

    // 访问数组元素
    println!("第一个元素: {}", numbers[0]);
    println!("第三个元素: {}", numbers[2]);

    // 修改数组元素
    let mut mutable_numbers = [10, 20, 30];
    mutable_numbers[1] = 25;
    println!("修改后的第二个元素: {}", mutable_numbers[1]);

    // 数组迭代
    println!("所有元素:");
    for number in numbers.iter() {
        println!("{}", number);
    }
}
```

## Loop

表示无限循环。

```rust
fn main() {
    let mut counter = 0;

    loop {
        println!("当前计数: {}", counter);
        counter += 1;

        if counter == 5 {
            break;
        }
    }
}
```

## Tuples

```rust
fn main() {
    // 创建一个包含两个元素的元组
    let person: (String, i32) = ("Alice".to_string(), 25);

    // 访问元组元素
    println!("姓名: {}", person.0);
    println!("年龄: {}", person.1);

    // 解构元组
    let (name, age) = person;
    println!("姓名: {}", name);
    println!("年龄: {}", age);

    // 创建带有命名字段的元组
    let point = (x: 10, y: 20);
    println!("X 坐标: {}", point.x);
    println!("Y 坐标: {}", point.y);

    // 元组作为函数返回值
    let result = get_person();
    println!("姓名: {}", result.0);
    println!("年龄: {}", result.1);
}

// 返回一个元组作为函数结果
fn get_person() -> (String, i32) {
    ("Bob".to_string(), 30)
}
```

## Strings

```rust
fn main() {
    // 创建一个字符串
    let greeting = String::from("Hello, Rust!");

    // 字符串长度和判空
    println!("字符串长度: {}", greeting.len());
    println!("字符串是否为空: {}", greeting.is_empty());

    // 连接字符串
    let name = "Alice";
    let message = format!("{} {}", greeting, name);
    println!("完整的问候消息: {}", message);

    // 字符串切片
    let name_slice = &message[7..12];
    println!("名字切片: {}", name_slice);

    // 字符串追加
    let mut greeting_mut = String::from("Hello");
    greeting_mut.push_str(", world!");
    println!("追加后的问候: {}", greeting_mut);

    // 字符串替换
    let replaced = greeting_mut.replace("world", "Rust");
    println!("替换后的问候: {}", replaced);

    // 字符串迭代
    println!("迭代字符:");
    for c in replaced.chars() {
        println!("{}", c);
    }

    // Unicode 标量值迭代
    println!("迭代 Unicode 标量值:");
    for scalar in replaced.chars().map(|c| c as u32) {
        println!("{}", scalar);
    }
}
```

## Casting

中文：类型转换。

用as关键词进行转换，类型转换并不总是可行的。在进行类型转换之前，应确保源类型和目标类型之间的转换是合法和有意义的，以避免潜在的数据丢失或错误。

```rust
let num1: u32 = 42;
let num2: i32 = num1 as i32;
```

使用From和Into trait进行转换：
Rust中的类型转换通常借助于From和Into trait，它们允许在类型之间进行自动转换。

```rust
rustCopy code
let num1: u32 = 42;
let num2: i32 = i32::from(num1);
```

## Enums 枚举类

首先已知枚举类和其它语言中的枚举有部分类似，枚举类包含着不同的“变体”。

```rust
enum Direction {
    North,
    East,
    South,
    West,
}
```

但是Rust的枚举类中每个变体可以有关联的数据或不关联的数据。枚举类型可以用于表示具有不同状态或选项的数据。

比如Option类型，可以表示有值或者没有值，而有值的时候则可以把具体的值表示出来。

```rust
enum Option<T> {
    /// No value.
    None,
    /// Some value of type `T`.
    Some(T),
}
```

## vector

vector类似array但是可以变长。

```rust
fn main() {
    // 创建一个空向量
    let mut numbers: Vec<i32> = Vec::new();

    // 添加元素到向量
    numbers.push(1);
    numbers.push(2);
    numbers.push(3);

    // 通过宏初始化向量
    let more_numbers = vec![4, 5, 6];

    // 访问向量元素
    println!("第一个元素: {}", numbers[0]);
    println!("最后一个元素: {}", numbers[numbers.len() - 1]);

    // 修改向量元素
    numbers[1] = 20;

    // 迭代向量
    println!("所有元素:");
    for number in &numbers {
        println!("{}", number);
    }

    // 向量长度
    println!("向量长度: {}", numbers.len());

    // 检查向量是否为空
    println!("向量是否为空: {}", numbers.is_empty());

    // 删除元素
    let removed_number = numbers.pop();
    println!("删除的元素
```

> 在这个示例中，我们展示了向量的各种操作：
> 
> - 首先，我们使用**`Vec::new()`**创建一个空的整数向量**`numbers`**，使用**`push()`**方法向向量中添加元素。
> - 我们还展示了使用**`vec![]`**宏来初始化向量**`more_numbers`**。
> - 使用索引访问向量的元素，并使用**`len()`**方法获取向量的长度。
> - 通过修改索引来修改向量的元素。
> - 使用**`for`**循环迭代向量中的元素。
> - 检查向量是否为空，使用**`is_empty()`**方法。
> - 使用**`pop()`**方法删除向量中的最后一个元素，并返回删除的元素。
> - 使用切片操作**`[..]`**，提取向量的部分元素。
> - 使用**`sort()`**方法对向量进行排序。
> - 使用**`clear()`**方法清空向量中的所有元素。
> 
> Rust的向量（Vector）是一种动态大小的数组，可以根据需要动态增长和缩小。向量可以存储相同类型的元素，并提供了丰富的方法和操作来处理和操作元素。向量的操作非常灵活，可以根据实际需求进行增删改查、排序、迭代和切片等操作。
> 
> 需要注意的是，向量只能存储相同类型的元素，一旦定义了向量的类型，就不能改变其元素类型。此外，向量的操作可能会涉及所有权和借用的概念，需要理解和遵守Rust的所有权规则。
> 

# 进阶语法