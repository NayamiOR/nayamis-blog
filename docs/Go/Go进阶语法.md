# 内建方法

内建方法：GO自带的方法，不需要引用包

## make 方法

作用：

- 创建slice, map, chan
- 返回**类型引用**

### make 切片

```python
mSlice := make([]string,length)
```

### make map

```python
mMap := make(map[int]string,length)
```

`map[int]string`花括号中是key的格式，后面是value的格式，length是容量，可以忽略

### make channel

```python
mChan := make(chan int)
```

## new 方法

与make 方法的区别：

- 内存置零
- 返回传入类型的**指针地址**

## append & delete & copy 方法

append & copy 针对 slice，delete 主要用于 map。

### append 方法

```go
mIDSlice := make([]int,2)
mIDSlice[0]=1
mIDSlice[1]=2
mIDSlice=append(mIDSlice,3)
```

此时这个数组一开始的len是2，cap是2。append以后len加一，但是cap变为4。

### copy 方法

```go
copy(SliceA,SliceB)
```

假设SliceA的长度是a，SliceB的长度是b。

如果a=b：

SliceA=SliceB

如果a>b：

将SliceA的前b项变为SliceB的前b项

如果a<b：

将SliceA的前a项变为SliceB的前a项

### delete 方法

```go
delete(A,B)
```

其中A是一个map，delete会在A中把key为B的键值对直接删除。

## panic & recover 方法

- panic 用于抛出异常
- recover 用于捕获异常

```go
panic("I am a panic!")
message := recover()
```

## len & cap & close 方法

- len → string, array, slice, map, chan
- cap → slice, array, chan
- close → chan

### close 方法

```go
func closeChan(){
	mChan := make(chan int,1)
	mChan <- 1
	close(mChan)
	//在项目中经常写成：defer close(mChan)，这样写在前面的话之后函数结束自动关闭，就不会忘记
	mChan <- 1 //这行会报错
}
```

# 结构体

声明时直接赋值结构体的语法糖：

```go
dog := Dog{ID:1,Name:"yaya",Age:2}
```

用new声明结构体：

```go
dog := new(Dog)
```

## 组合

可以用来实现面向对象中继承的特性

```go
type Animal struct{
	colour string
}

type Dog struct{
	Animal
	ID int
	Name string
}
```

上文中在Dog结构体内部第一行写了Animal，就可以把Animal看作Dog的父类，可以使用Animal的属性和方法

## 作用域

包中，大写的结构体，结构体中大写的属性和方法才可以被外部访问，Go语言通过大小写来判断包内部的内容是否可以被外部访问。

# 接口

涉及到面向对象中抽象、封装、多态的特性。

## 定义接口

定义一个接口：

```go
type Behavior interface{
	Run string
	Eat string
}
```

定义一个Dog类，加入对应的方法

```go
type Dog struct {
	ID   int
	Name string
	Age  int
}

func (d *Dog) Eat() string {
	return "eating"
}

func (d *Dog) Run() string {
	return "running"
}
```

![[Pasted image 20230911145635.png]]

此时可以看到已经判定为Dog类实现了Behavior接口（隐式实现）。

## 多态

测试接口变量定义：

```go
var b TryInterface.Behavior
	b = new(TryInterface.Dog)
```

此时定义的b的类型是接口Behavior（TryInterface是包名）

在方法中利用接口：

```go
func action(b TryInterface.Behavior) string {
	b.Run()
	b.Eat()
	return ""
}
```

在这个例子中，传入的参数b可以是任何实现了接口Behavior的结构体，比如Dog。 方法中会调用 传入的结构体对应的Run和Eat方法。

# 并发

## 协程

启动协程只需要用到`go`关键字。

定义一个方法和一个主函数：

```go
func Loop() {
	for i := 0; i < 10; i++ {
		time.Sleep(time.Microsecond * 10)
		fmt.Printf("%d ", i)
	}
}

func main() {
	go GoRoutine.Loop()
	go GoRoutine.Loop()
	time.Sleep(time.Second * 5)
}
```

输出如下

```go
0 0 1 1 2 2 3 3 4 4 5 5 6 6 7 7 8 8 9 9
```

说明go协程是同时运行的

**p.s.** 以上代码中`time.Sleep`的作用是：

1. 让程序关闭的慢一点，留出给协程输出的时间
2. 在协程的输出间留一点空隙给另外一个协程，体现出协程同时运行的特点

### 设置最大核心数

在程序的开头部分加上如下代码可以限制程序占用的最大核心数：

```go
runtime.GOMAXPROCS(runtime.NumCPU())
```

`runtime.NumCPU()`表示全部的CPU数量。`GOMAXPROCS`函数传入的参数决定了程序用多少核心，如上文就是全部CPU。

## 协程通信

- channel：可以看作是管道，用于在协程之间进行数据交互
- select 方法：与 switch 方法类似，但是 case 语句必须是 io 操作，通常是从 channel 中获取数据

### channel

**创建 channel**

以下代码创建了一个名为`chanInt`的 channel，数据类型是整型，且缓存是10：

```go
var chanInt chan int = make(chan int,10)
```

令两个方法发送传输数据进入`chanInt`：

```go
func Send(){
	chanInt <- 1
	chanInt <- 2
	chanInt <- 3
}

func Receive(){
	num := <- chanInt
	fmt.Println(num)
	num := <- chanInt
	fmt.Println(num)
	num := <- chanInt
	fmt.Println(num)
}

func main(){
	go Send()
	go Receive()
	time.Sleep(time.Second * 60)
}
```

输出如下：

```go
1
2
3
```

### select 方法

可以在方法中选多个不同的 channel 赋值：

```go
for{
	select{
		case num := <-chanInt:
			fmt.Println(num)
	}
}
```

如果在代码中不需要赋值给变量，可以把上文中 num 的位置的变量直接删去，变成：

`case <-chanInt:`

## 协程同步

系统工具 `sync.WaitGroup`

- Add(delta int) 添加协程记录
- Done() 移除协程记录
- Wait() 同步等待所有记录的协程全部结束

创建 WaitGroup：

```go
var WG sync.WaitGroup
```

读写函数示例以及main函数：

```go
func Read(){
	for i:=0;i<3;i++{
		WG.Add(1)
	}
}

func Write(){
	for i:=0;i<3;i++{
		time.Sleep(time.Second*2)
		WG.Done()
	}
}

func main(){
	Read()
	go Write()
	WG.Wait()
	fmt.Println("All Done")
}
```

main函数：

1. 先用主线程读取（`Read()`）
2. 在协程里写入（`go Write()`）
3. 在写入之后把协程记录删除（`WG.Done()`）
4. 在主线程里等待全部完成（`Wait()`）
5. 然后继续进行后续的操作（输出）

# 指针

## 基本使用

```go
var count int = 20
var countPointer *int
countPointer = &count
```

没有赋值过的指针变量的值为0或nil。

## 指针和数组

### 指针数组

```go
a,b := 1,2
pointArr := [...]*int{&a,&b}
```

这里的`pointArr`是一个数组，存放的类型是指针变量。

### 数组指针

```go
arr := [...]int{3,4,5}
arrPoint := &arr
```

这里的`arrPoint`是一个指针，指向一个数组。

# JSON序列化

是官方提供的数据包，可以序列化和反序列化数据。

## 序列化

- 结构体序列化
- Map序列化

### 结构体序列化

```go
type Server struct{
	ServerName string
	ServerIp string
	ServerPort int
}

func Serialize(){
	server := new(Server)
	server.ServerName = "Demo"
	server.ServerIp = "127.0.0.1"
	server.ServerPort = 8080
	b,err := json.Marshal(server) //序列化成json字节数组
	if err != nil{
		fmt.Println(err.Error())
		return
	}
	fmt.Println(string(b)) //将json字节数组转换成string
}
```

输出：

```go
{"ServerName":"Demo","ServerIp":"127.0.0.1","ServerPort":8080}
```

### Map序列化

```go
func SerializeMap() {
	server := make(map[string]interface{})
	server["Servername"] = "Demo"
	server["ServerIp"] = "198.0.0.1"
	server["ServerPort"] = 8080
	b, err := json.Marshal(server)
	if err != nil {
		fmt.Println(err.Error())
		return
	}
	fmt.Println(string(b))
}
```

输出：

```go
{"ServerIp":"198.0.0.1","ServerPort":8080,"Servername":"Demo"}
```

---

在定义结构体的时候可以用如下的写法

```go
type Server struct{
	ServerName string `json:"name"`
	ServerIp string `json:"ip"`	
	ServerPort int `json:"port"`
}
```

这种写法的作用是，在json序列化时把数据名从前面的属性名映射成后面单独规定的名字。

## 反序列化

系统方法：

```go
func Unmarshal(data []byte,v interface{}) error
```

### 反序列化为结构体

```go
func DeSerializeStruct() {
	jsonStr := `{"name":"Demo","ip":"198.0.0.1","port":8080}`
	server := new(Server)
	err := json.Unmarshal([]byte(jsonStr), &server)
	if err != nil {
		fmt.Println(err.Error())
		return
	}
	fmt.Println(server)
}
```

### 反序列化为Map

```go
func DeSerializeMap() {
	jsonStr := `{"name":"Demo","ip":"198.0.0.1","port":8080}`
	server := make(map[string]interface{})
	err := json.Unmarshal([]byte(jsonStr), &server)
	if err != nil {
		fmt.Println(err.Error())
		return
	}
	fmt.Println(server)
}
```

# 语法糖

## `…`可变参数

```go
func Sugar(values...string){
	for _,v := range values{
		fmt.Println("v:",v)
	}
}
```

以上这个函数的参数是多个string类型的值，在函数的运行中这不定个值会放到values这个数组里面，也就是说变长参数在运行中的本质是数组。

# Module

## 介绍

三部分：

- 集成在go命令里的工具集：提供了八个命令
- go.mod文件：保存所有依赖列表
- go.sum文件：版本管理文件，保存不同版本对应哈希。用于校验依赖，避免恶意修改

### go.mod

假设我们在文件中引用了一个在线工具库：

```go
import("github.com/hashicorp/golang-lru")
```

go.mod结构如下：

```go
module 你当前的module名
go 1.12 （你的go版本）
require github.com/hashicorp/golang-lru v0.5.3
```

go.mod下一级的go.sum程序里存储着`"github.com/hashicorp/golang-lru"`的哈希信息。

### 命令

以下命令前面都需要加go mod，格式如下：

```go
go mod graph
```

- init：初始化工程生成go.mod
- build：编译工程生成exe
- graph：输出工程所有的依赖
- download：下载依赖
- tidy：添加需要的依赖，删除不需要的依赖
- verify：验证依赖
- why：展示一些依赖关系
- edit
- vendor

![[Pasted image 20230911145541.png]]

小结：

![[Pasted image 20230911145814.png]]