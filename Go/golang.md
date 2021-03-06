## golang

###  常用命令


- `go get` 获取远程包

- `go run` 运行项目

- `go build` 测试编译 检查是否有编译错误

- `go fmt` 格式化编码 

- `go install` 编译包文件并编译整个项目

- `go test` 运行测试文件 （测试文件是结尾带_test 文件 如 GolangList_test.go 

- `go doc` 查看文档 如 查询一个语法的用法 格式如：`go doc fmt`

### 交叉编译

- 在window 编译一个linux(MAC 平台可执行的文件

```
SET CGO_ENABLED=0
SET GOOS=linux SET
GOARCH=amd64

```

### % 标识符golang

- %v 用法 `fmt.Printf("%v", 变量) // 变量`
- %T 检测数据类型 `fmt.Printf("%T", 变量) // 数据类型 如string int等`
- %02d 转换数据2位 %04d 转换4位
- %d int类型
- %f float类型
- %t bool类型
- %s 输出字符串
- %q 双引号包裹的字符串 有go语法安全转义

### 知识点

- golang没有三元运算符

- := 和 = 的差别 := 是声明了变量并赋值 =是赋值变量

- := 简短声明的变量只能在函数内使用

- 在一个go程序里如果有init函数先执行init函数在执行main函数
`func init () {}
func main () {}`

- _下划线用处 一个函数返回多个值 但你只想用一个 在go的机制里 每个返回值和变量都要用到 要不就报错 这时_下划线的作用就来的 占位
案例如下

```gotemplate
    func foo () (int, string) {
        return 1, '字符串'
    }
    func main () {
        a,_ := foo(); // 1
        _,b := foo(); // 字符串
    }
```
- 变量和常量批量创建 如下

```gotemplate
    var (
        a = 1 // go的变量机制 如果有未定义的变量默认上一个变量的值
        b // 1
        c // 1
    )
 // go的iota 没const出现初始化为0 每出现一个const值就+1
    const (
        a  = iota // 0
        b // 1
        c // 2
    )
    // 它是新的const常量所以初始化为0
    const (
        a = iota // 0
        b // 1
        c // 2
    )
    // iota在一行值相同

    const (
        a iota // 0
        b,c iota // 1,1
    )

    const (
        z1 = iota // 0
        z2 = 100 // 100
        z3 = iota // 2
    )

```

- 测试文件声明 commodityList_test.go  只要带着_test后缀就是测试文件
### sort包

```cassandraql
s3 := []int {1,2,0,4}

	sort.Ints(s3)

	fmt.Println(s3)
// s3 = [0 1 2 4]

```
### if

- if 判断流 if支持在条件里声明变量 如下

```gotemplate
    // 基础if
    a := 1 
    if a == 1 {
        // true
    } else {

    }
    // if支持在条件里声明变量 

    if a := 1; a == 1 {
        code
    }

```

### for 循环

- 案例1

```gotemplate
    // 基础用法
    for a := 0; a < 10; a++ {
        code
    }
    // go 没有while 用for解决如下
    a := 0
    for a != 10 {
        a++
    }

    // for遍历map和array的写法
    // 声明一个数组
    list := []int{1,2,3,4}

    for index, val := range list {
        // index 当前索引 val 当前值
    }
    // range 类似其他语言的forEach 获取他的index 和 value 如下

```

### break和continue 

- break 跳出判断 循环

- continue 忽略剩余的循环体而直接进入下一次循环的过程

### 定义map 

- var mapData map[string]string   map[数据类型]数据类型
mapData = make(map[string]string) make分配内存
mapData["name"] = "zeyv"

fmt.Println(mapData) // ["name":"zeyv"]

### runtime库

- runtime.GOOS 检测操作系统
- runtime.Caller(1) 检测当前文件

### time库

- time.Now() 当前的时间

- time.Now().Day() // 当前天 Mouth Year 月年

- UTC 通用协调世界时间 如Wed Dec 21 08:52:14 +0000 UTC 2011
 

- 示例 计算函数运行时间 用到了time的 Now()和Sub()

```gotemplate
    start := time.Now()
    test()
    end := time.Now()
    times := end.Sub(start)
```

### os库

- os.Getenv 检测环境变量

### strings 库

- 判断前缀是否含有这个字符 返回bool strings.HasPrefix(str, "匹配的字符")

- 判断后缀是否包含这个字符 返回bool strings.HasSuffix(str, '匹配的字符')

- 判断是否包含这个字符 返回bool strings.Contains(str, "字符串里的任意字符")

- 查询字符串的位置 返回索引 string.Index(str, "查询的字符") -1 表示字符串不包含这个元素
- 查询最后出现位置的索引 返回索引 string.LastIndex(str, "查询的字符")-1 表示字符串不包含这个元素

- 替换字符 string.Replace(str, old,new,num) // str 字符串 old 老数据 new新数据 num 替换几个

- 统计字符串出现的次数 返回number strings.Count(str, "匹配的字符")

- 重复字符串返回新的字符串 strings.Repeat(str, 次数num)

- 转换大小写
    ToLower(str) // 小写
    ToUpper(str) // 大写

 - 修剪字符串 可以使用strings.TrimSpace(Str) 删除开头和结尾的空白符号 如果要制定字符要用strings.Trim(str, "指定字符") 如果想删除开头和结尾 使用strings.TrimLeft strings.TrimRight来实现
- 分割数组 strings.Fields(str) 根据一个或多个空白符号分割 返回一个slice

- 指定分割字符 strings.Split(str, "指定字符") 返回slice

- Join 用于将元素类型为 string 的 slice 使用分割符号来拼接组成一个字符串 todo*

- strings 4.7.11 再看看

### strconv 用于字符串转换包

- strconv.Atoi(s string) 用于把string类型转换成int类型
- strconv.ParseFloat(s string) 用于把string类型转换成Float64位类型
- strconv.Itoa(i int) 用于把int类型转换成字符串十进制
- strconv.FormatFloat(f float64, fmt byte, prec int, bitSize int) string 将 64 位浮点型的数字转换为字符串，其中 fmt 表示格式（其值可以是 'b'、'e'、'f' 或 'g'），prec 表示精度，bitSize 则使用 32 表示 float32，用 64 表示 float64。
- strconv.intSize 获取程序运行的操作系统平台下int类型所占的位数 类似64位系统输出64

### switch 

-
golang 特点不需要break来表示结束
如果在执行完每个分支的代码还想继续执行的话用fallthrough

 ```gotemplate
   // 例子一
    var a int = 1
	switch a {
	case 1:
		fmt.Println("a1")
	case 2:
		fmt.Println("a2")
	case 3:
		fmt.Println("a3")
	default:
		fmt.Println("a4")
	}
	
    // 例子二
    var b int = 1
	switch {
	case b >= 1:
		fmt.Println("b1")
        fallthrough
	case b >= 2:
		fmt.Println("b2")
        fallthrough
	case b >= 3:
		fmt.Println("b3")
        fallthrough
	default:
		fmt.Println("b4")
	}

   // 输出b4
```

### fmt库 输出 log

- Println Println等

- Scanf 阻塞等待用户输入 如下

```gotemplate
    var a int 
    fmt.Scanf("%d\n", &a) //说明当检测到\n回车后，解析输入的格式化内容
```


### func 函数
 
 ```gotemplate
    // 函数命名方式在golang里是驼峰式开头小写 开头大写则可以在包外引入使用
    func main () {

    }
```
- 多个返回值de时候要加() 类似(int,int)

- 可以传递函数 类似 callback(1,add)

```gotemplate
func main () {
    callback(1, add)
}

func add (a,b int) {
    fmt.Println(a,b,a+b) // 1 3 4
}

func callback (y int, f (int, int)) {
    f(y, 3)
}
```

- 闭包

```gotemplate

func main () {
    // 用法一
    func (y string) {
        fmt.Println(y) // str
    }("str")
    // 用法二

    s  := func (a,b int) int {return a + b}
    s(1,2) // 3

}


// 工厂函数

func main () {
    pppp := Hz(".jpg")
	fmt.Println(pppp("file")) // file.jpg
}

func Hz(str string) func(a string) string {
	return func(name string) string {
		if !strings.HasSuffix(name, str) {
			name += str
		}
		return name
	}
}

// 计算函数执行时间

start := time.Now()
test()
end := time.Now()
times := end.Sub(start)
fmt.Printf("times = %d\n", times) // 执行的时间
```

### golang 关键字 defer

- 延迟调用 defer后面必须是函数调用，语句要不 会报错 
- 当前方法完成后执行的

- 执行路径是从上往下

- 案例一

```gotemplate
    func test1 () {
        for i := 0; i < 5; i++ {
            defer fmt.Printf(i) // 4 3 2 1 0
        }
    }

```

- 案例二

```gotemplate
    # 关闭文件流
    defer file.Close()

    # 解锁一个加锁的资源
    mu.Lock()
    defer mu.Unlock()

    # 打印最终报告
    printHeader()
    defer printFooter()

    # 关闭数据连接
    defer disconnectFromDB()
```

### cap和len区别 

- len()查看数组或slice的长度

- cap() 查看的是数组或slice的容量 案例如下



```gotemplate
    a := []int {1,2,3}
    b := a[1,2]

    // len(b) // 1
    // cap(b) // 3

```
### make 创建切片

- make([]type, len, cap) // cap可选参数

```gotemplate
    a := make([]int, 10, 20) // len 10 cap 20
```

### new() 和 make() 的区别 7.2.4


### bytes 包

### 指针 &*


- &取地址 *取地址值

- 指针变量通常是ptr

- 空指针 nil

- 案例如下
# 注意事项 
- 不能获取到常量和字面量的地址 (const 数字11)
- 带类型的要加* 如 var a *string

```gotemplate
    s := 'sdsdsd'

    var a *string = &s //取s的当前内存地址

    var b = *a // 'sdsdsd'

    fmt.Println(b, *a) // b,*a 取出s内存地址的值 输出'sdsdsd'

    s := 'sdsdsd'

    var a *string = &s // 去s的当前内存地址
    *a = "sss" // 改变指针内存地址值
    var b = *a // 'sdsdsd'
    fmt.Println(b, *a) // b, *a 取出s内存地址的值 输出sss

    // 函数应用

    func main () {
        n := 1
        test(&n, 1)
    }
    
    func test(a *int, b int) int {
        fmt.Println(a, b, *a) //0xc000010110 1 1
        *a = 2 // 修改指针值
        fmt.Println(a, b, *a, "修改") // 0xc000010110 1 2 修改
        return *a + b
    }
```
### go 结构体 

- 声明 
```gotemplate
type person struct {
    Name string
    Age int
    ....
}

func main () {
    // 初始化时就获取地址
    a := &person{
        Name: '11',
        Age: 23
    }
    a.Name = 'zeyv' // go修改结构体不用加*获取指针就能获取到值
}
```

- 匿名结构体 
```gotemplate
func main () {
    a:=&struct {
        Name string
        Age int
    } {
        Name: '11',
        Age: 22
    }
}
```

- 结构体里面包含匿名结构体 怎么初始化
```gotemplate
type persong struct {
    Name string
    Age int
    Contat struct {
        Phone, City int
    }
}
func main () {
    a:=&persong {
         Name: '11',
        Age: 22
    } 
    a.Contat.Phone = 1111
    a.Contat.City = 1111
}
```

- 结构体 匿名字段
```gotemplate
type persong struct {
     string
     int
}
func main () {
    // 初始化
    a:=&persong {'11',22} 
}
```

- go不存在继承 有组成

- 组成 结构体

```gotemplate
type test1 struct {
    Sex int
}

type test2 struct {
    test1
    Name string
}

type test3 struct {
    test1
    Name string
}

func main () {
    a := test2{
        Name: '1',
        test1:test1{Sex: 1} // 初始化方式1
    }
    a.Sex = 1 // 初始化方式2 go的机制 只要把结构体放到另一个结构体里就有组成 类似如下
    // type test2 struct {
        test1 包含Sex test2 也有Sex这个属性
    }
}
```


### goto


### 接口interface

```gotemplate
 type name interface {
    Name () string
    connect()
}

type name struct {
    name string
}

func (n *name) Name () string {
    fmt.Println(n.name)
}

func (n *name) connect () string {
    fmt.Println(‘连接成功’)
}

func main () {
 // 初始化结构体
 a := name{"11"}
 a.connect()
}
```
### go mod(modules)
+ 开启modules和gopoxy设置
    + go env -w GO111MODULE=on
    + go env -w GOPROXY=https://goproxy.cn,https://goproxy.io,direct

### golang框架

* 先go get 框架地址

* 然后在go mod init go框架

* 再go mod edit -require 框架github地址
### 内存缓存

### 导包需要再看下 package xx

### beego框架知识点

- 根据bee工具 初始化beego项目 go get github.com/astaxie/bee 然后bee new 项目名称 运行用 bee run
- 注册路由  beego.Router(路径, 指针结构如 &models.Home{})

- 获取conf里的配置信息 bee.AppConfig.string("参数名")  bee.AppConfig.string string是获取类型如果是int就用int()

- 获取conf里的配置信息 也可以用beego自带的默认参数的形式获取 如下

- beego模板使用 tpl 如下案例

- 注册结构体 orm.RegisterModel(new(结构体名称), ...)
	
- 注册驱动 orm.RegisterDriver(驱动名称,orm.DRSqlite)
	
- todo  orm.RegisterDataBase("default", 驱动名称,数据库名称, 10) 连接数据库 数据库名称 驱动名称 数据库的路径 最大连接数

```gotemplate
//  嵌套输出 用with关键字
<div>
    {{.User.name}}{{.User.Age}}{{.User.Sex}} // User这个字段用了3次 为了解决咱们用with关键字
</div>
<div>
    {{with User}}
    {{.name}}{{.Age}}{{.Sex}}
    {{end}}结构图 
</div>


// 循环输出 用range
<div>
    {{/*Nums的数据结构是[1,2,3,4,5,6,7]*/}}
    {{range Nums}}
    {{.}}
    {{end}}
</div>

// 模板函数 
// 模板变量
{{$tplVar := .TplVar}}
{{$tplVar}}
// 输出html
{{str2html .Html}}   
// html 编码的形式显示
{{.Pipe | htmlquote}}
// 模板嵌套 复用同样的组件

// 定义这是
{{define "test"}}
<div>
this is template
</div>
{{end}}
// 用的时候直接如下
{{template "test"}}
// 如果模板里有逻辑操作后面再加一个点 如下
{{template "test" .}}
```

```gotemplate
// 默认golang conf参数名
beego.AppName beego.HttpPort // int类型的httpPort beego.RunMode
```  
- 重定向 this.Redirect(url,code码)
- 设置cookie  this.ctx.setCookie(cookiename,cookievalue,存储时间,url地址 ) 存储时间清空的话设置-1
- 提取cookie  this.ctx.Request.Cookie(cookiename)

- beego日志级别 

- orm使用 创建数据表等
```
    orm.Debug = true // 开启 ORM 调试模式
    orm.RunSyncdb("default", false, true) // todo 自动建表 数据库名称 是否一直重新建表 是否打印相关信息 开发默认都是true
    o := orm.NewOrm() // 创建orm数据库
    o.Insert() // 插入
    o.Delete() // 删除
    o.Using(切换的数据库名称) // 切换的数据库 
    
    qs := o.QueryTable(表名) // 查询数据表
    qs.All(&data) // 返回对应结果集对象
    qs.Filter("title",name).One(cate) // 查询数据库里有没有这个name 用来过滤查询结果，起到 包含条件 的作用 多个 Filter 之间使用 AND 连接
    strconv.ParseInt(id,10,64) // string转换成int60位十进制
```

### mysql

* mysql
