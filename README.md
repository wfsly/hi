# Hi

go mod 测试

1. 在`GOPATH`之外创建一个文件夹, 例如hi
2. 创建hi.go, 包名就是hi
3. 在目录下执行`go mod init github.com/wfsly/hi`, 此时会生成一个go.mod文件，里面会包含go包名和go版本
```
module github.com/wfsly/hi

go 1.13
```
4. 将包用git初始化，提交代码，并生成一个v1.0.0的tag, 然后再github创建项目，将代码和tag都push远程分支。
这样之后就可以在其他go项目中import 此包使用，编译找不到包时，可用
`go get -u -v github.com/wfsly/hi`去下载此包

5. 通过新建一个项目hello，通过`go mod init hello`,将其初始化支持module功能
6. 然后在代码中import刚创建的hi包,之后执行`go build`会自动分析项目依赖并下载. 会有如下输出
```
go: finding github.com/wfsly/hi v1.0.0
go: downloading github.com/wfsly/hi v1.0.0
go: extracting github.com/wfsly/hi v1.0.0
```

并且会在go.mod中加入hi包名和版本
```
module hello

go 1.13

require github.com/wfsly/hi v1.0.0
```
