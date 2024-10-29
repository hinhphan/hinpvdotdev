# Router

# Controller

+ Ví dụ nội dung file example.controller.go
```go
...
type ExampleController struct {
    exampleService *service.ExampleService
}

func NewExampleController() *ExampleController {
    return &ExampleController {
        exampleService: service.NewExampleService(),
    }
}

func (ex *ExampleController) ExampleFunc(c *gin.Context) {
    ...
}
...
```

+ Luồng gọi request => controller => service => repo => models => DB

# Service

# Repo

# ...