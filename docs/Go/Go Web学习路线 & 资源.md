# 语言入门&进阶

[Go语言简明教程](https://link.zhihu.com/?target=https%3A//geektutu.com/post/quick-golang.html) 和 [Go Test 简明教程](https://link.zhihu.com/?target=https%3A//geektutu.com/post/quick-go-test.html) 快速入门。

进阶推荐 [Go 语言高性能编程](https://link.zhihu.com/?target=https%3A//geektutu.com/post/high-performance-go.html)。

# 开源库（Github：7days-golang）

进步最快的方式是找一些经典的开源库学习，这样能够最快地学到 Go 语言在实际中是如何应用的。推荐 [7days-golang](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang) 这个项目，每次花七天时间模仿一个经典库的实现。这些库的代码规模一般比较大，因此选取了最重要的特性，拆分为7天实现，每天的代码都是独立文件夹保存的，每个子项目代码规模均在 500 行左右，非常适合进一步学习。目前已经实现：

### [Gee](https://link.zhihu.com/?target=http%3A//geektutu.com/post/gee.html)：模仿 gin 实现的 Web 框架。

- [第一天：前置知识(http.Handler接口)](https://link.zhihu.com/?target=https%3A//geektutu.com/post/gee-day1.html)，[Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-web)
- [第二天：上下文设计(Context)](https://link.zhihu.com/?target=https%3A//geektutu.com/post/gee-day2.html)，[Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-web)
- [第三天：Tire树路由(Router)](https://link.zhihu.com/?target=https%3A//geektutu.com/post/gee-day3.html)，[Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-web)
- [第四天：分组控制(Group)](https://link.zhihu.com/?target=https%3A//geektutu.com/post/gee-day4.html)，[Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-web)
- [第五天：中间件(Middleware)](https://link.zhihu.com/?target=https%3A//geektutu.com/post/gee-day5.html)，[Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-web)
- [第六天：HTML模板(Template)](https://link.zhihu.com/?target=https%3A//geektutu.com/post/gee-day6.html)，[Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-web)
- [第七天：错误恢复(Panic Recover)](https://link.zhihu.com/?target=https%3A//geektutu.com/post/gee-day7.html)，[Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-web)

### [GeeCache](https://link.zhihu.com/?target=http%3A//geektutu.com/post/geecache.html)：模仿 groupcache 实现的[分布式缓存](https://www.zhihu.com/search?q=%E5%88%86%E5%B8%83%E5%BC%8F%E7%BC%93%E5%AD%98&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A1018940882%7D)。

- 第一天：[LRU 缓存淘汰策略](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geecache-day1.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-cache)
- 第二天：[单机并发缓存](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geecache-day2.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-cache)
- 第三天：[HTTP 服务端](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geecache-day3.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-cache)
- 第四天：[一致性哈希(Hash)](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geecache-day4.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-cache)
- 第五天：[分布式节点](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geecache-day5.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-cache)
- 第六天：[防止缓存击穿](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geecache-day6.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-cache)
- 第七天：[使用 Protobuf 通信](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geecache-day7.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-cache)

### [GeeORM](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geeorm.html)：模仿 gorm 实现的 ORM 框架

- 第一天：[database/sql 基础](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geeorm-day1.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-orm)
- 第二天：[对象表结构映射](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geeorm-day2.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-orm)
- 第三天：[记录新增和查询](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geeorm-day3.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-orm)
- 第四天：[链式操作与更新删除](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geeorm-day4.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-orm)
- 第五天：[实现钩子(Hooks)](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geeorm-day5.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-orm)
- 第六天：[支持事务(Transaction)](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geeorm-day6.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-orm)
- 第七天：[数据库迁移(Migrate)](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geeorm-day7.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-orm)

### [GeeRPC](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geerpc.html)：模仿 net/rpc 实现的 RPC 框架

- 第一天 - [服务端与消息编码](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geerpc-day1.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-rpc)
- 第二天 - [支持并发与异步的客户端](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geerpc-day2.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-rpc)
- 第三天 - [服务注册(service register)](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geerpc-day3.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-rpc)
- 第四天 - [超时处理(timeout)](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geerpc-day4.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-rpc)
- 第五天 - [支持HTTP协议](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geerpc-day5.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-rpc)
- 第六天 - [负载均衡(load balance)](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geerpc-day6.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-rpc)
- 第七天 - [服务发现与注册中心(registry)](https://link.zhihu.com/?target=https%3A//geektutu.com/post/geerpc-day7.html) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/tree/master/gee-rpc)

### [Wasm](https://link.zhihu.com/?target=https%3A//geektutu.com/post/quick-go-wasm.html)：Go Webassembly 的一些 demo

- 示例一：Hello World | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/blob/master/demo-wasm/hello-world)
- 示例二：[注册函数](https://www.zhihu.com/search?q=%E6%B3%A8%E5%86%8C%E5%87%BD%E6%95%B0&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A1018940882%7D) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/blob/master/demo-wasm/register-functions)
- 示例三：操作 DOM | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/blob/master/demo-wasm/manipulate-dom)
- 示例四：[回调函数](https://www.zhihu.com/search?q=%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A1018940882%7D) | [Code](https://link.zhihu.com/?target=https%3A//github.com/geektutu/7days-golang/blob/master/demo-wasm/callback)

---

# Go学习路线图

[https://github.com/Alikhll/golang-developer-roadmap](https://github.com/Alikhll/golang-developer-roadmap)

[golang-developer-roadmap/ReadMe-zh-CN.md at master · Alikhll/golang-developer-roadmap](https://github.com/Alikhll/golang-developer-roadmap/blob/master/i18n/zh-CN/ReadMe-zh-CN.md)

![[Pasted image 20230911145856.png]]

![[Pasted image 20230911145909.png]]
---

[有没有推荐的golang的练手项目？ - 知乎](https://www.zhihu.com/question/369863905/answer/2017788619)