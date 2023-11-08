一般在工程中会把路由文件放在单独的文件夹里，然后在main.go中监听时，调用路由文件。以下是做法：

要在main.go中监听多个路由文件，可以按照以下步骤操作：

1. 在项目中创建多个路由文件，例如router1.go和router2.go。
2. 在每个路由文件中，创建gin路由并定义处理程序。例如：

```go
package handlers

// router1.go
import "github.com/gin-gonic/gin"

func setupRouter1() *gin.Engine {
	r := gin.Default()
	r.GET("/", func(c *gin.Context) {
		c.JSON(200, gin.H{
			"message": "Hello World from Router 1",
		})
	})

	return r
}

//router2.go
package main

import "[github.com/gin-gonic/gin](<http://github.com/gin-gonic/gin>)"

func setupRouter2() *gin.Engine {
	r := gin.Default()
	r.GET("/hello", func(c *gin.Context) {
	c.JSON(200, gin.H{
		"message": "Hello from Router 2",
	})
})

return r
}
```

1. 在main.go文件中导入所有的路由文件并使用gin的Group()方法将它们组合在一起。例如：

```go
package main

func main() {
	r := gin.Default()
	// 导入所有路由文件并使用 gin 的 Group() 方法将它们组合在一起
	r1 := setupRouter1()
	r2 := setupRouter2()
	
	r.Group("/router1").Use(r1.Routes())
	r.Group("/router2").Use(r2.Routes())
	
	r.Run(":8080")
}
```

上面的代码导入了router1.go和router2.go文件，并使用Group()方法将它们组合在一起。最后，代码将服务器运行在localhost:8080上。

现在可以从终端中使用以下命令运行代码：

go run main.go

这将启动服务器，并在浏览器中访问 `http://localhost:8080/router1/` 和 `http://localhost:8080/router2/hello` 可以分别看到页面上显示：
	"Hello World from Router 1"和"Hello from Router 2"。