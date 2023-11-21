# 我自用的二分查找算法推荐

在此分享一下我自用的二分查找方法，这里只说用法，不说原理，原理请看下面的链接。

## 原思路

[【二分查找为什么总是写错？】](https://www.bilibili.com/video/BV1d54y1q7k7/?share_source=copy_web&vd_source=ee5f5f62deebaad2520d5495cba1bc3f)

## 我的理解与总结

### 边界规划

`a` 从 `-1` 开始，`b` 从 `len(arr)` 开始

也就是说，答案被夹在 `a` 和 `b` 之间，而 `a` 和 `b` 是不可能取到的。而且在整个过程中，`a` 和 `b` 都表示不会被取到，而有效区间一直夹在 `a` 和 `b` 之间。

### 循环条件

使用 `while` 循环，循环条件为 `a+1<b`，也就是说，当 `a` 和 `b` 相邻时，循环结束。

### 取中间值

取中间值的操作和其它二分大同小异，个人使用：

```python
mid = (a+b)>>1
```

讲究的可以使用：

```python
mid = a + (b-a)>>1
```

### 判断与转移

用二分把数组变成两部分，一部分是满足的，一部分是不满足的。

判断时，不满足的情况中，太大或者太小可以按一般的二分查找的思路来。

如果遇到刚好要求的情况，可以直接返回，但我一般会这么做：

我会在满足要求时，依旧移动上下界的指针中的一个，比如要求第一个大于等于某数的值时，就可以这样：

```python
if arr[mid]>=target:
    b = mid
else:
    a = mid
return b
```

总之按这样的逻辑，最后 `a` 和 `b` 会相邻，而且 `a` 指向的是第一个小于某数的值，`b` 指向的是第一个大于等于某数的值。

根据实际情况的不同，绝大多数情况下，`a` 是小于某数，`b` 是大于某数。对于等于某数的情况，从 `if` 的逻辑来判断，比如 `if arr[mid]>=target`，那么等于某数的情况下会把 `b` 移动到 `mid`，而 `a` 不会移动，所以 `a` 指向的是第一个小于某数的值，`b` 指向的是第一个大于等于某数的值。反之，使用 `if arr[mid]>target`，那么等于某数的情况下会把 `a` 移动到 `mid`，而 `b` 不会移动，所以 `a` 指向的是第一个小于等于某数的值，`b` 指向的是第一个大于某数的值。

换成别的题目，最后答案也肯定会在 `a` 和 `b` 之间，具体是哪个则取决于你的设置。

如果遇到无解的二分，比如要求第一个大于某数的值，但数组中没有大于某数的值会怎么样呢？

已知最后 `a` 和 `b` 会相邻，而我们提前定义了 `b` 作为最后返回的正确值。所以在无解的情况下，`b` 不会被移动，它的值会一直是 `len(arr)`，而 `a` 会被移动到 `len(arr)-1`，所以最后返回的是 `len(arr)`，这是一个不可能取到的值，所以可以用来判断是否有解。

### 整体代码

#### Python

```python
def binary_search(arr,target):
    a = -1
    b = len(arr)
    while a+1<b:
        mid = (a+b)>>1
        if arr[mid]>=target:
            b = mid
        else:
            a = mid
    return b
```

#### C++

```cpp
int binary_search(vector<int>& arr,int target){
    int a = -1;
    int b = arr.size();
    while(a+1<b){
        int mid = (a+b)>>1;
        if(arr[mid]>=target){
            b = mid;
        }else{
            a = mid;
        }
    }
    return b;
}
```

#### Java

```java
int binary_search(int[] arr,int target){
    int a = -1;
    int b = arr.length;
    while(a+1<b){
        int mid = (a+b)>>1;
        if(arr[mid]>=target){
            b = mid;
        }else{
            a = mid;
        }
    }
    return b;
}
```

#### Go

```go
func binary_search(arr []int,target int) int{
    a := -1
    b := len(arr)
    for a+1<b{
        mid := (a+b)>>1
        if arr[mid]>=target{
            b = mid
        }else{
            a = mid
        }
    }
    return b
}
```
