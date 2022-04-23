# 包fmt的常见使用

标准库中的fmt包可以格式化字符串和从字符串中解析数据。

#### 基本的fmt

* Print、Println、Printf

```go
n, err := fmt.Print("Hello World")          // n = 11 输出：Hello World
n, err := fmt.Println("Hello World")        // n = 12 输出：Hello World\n
n, err := fmt.Printf("Hello %s", "World")   // n = 11 输出：Hello World
```

* Sprint、Sprintln、Sprintf

```go
str, err := fmt.Sprint("2 words") // returns string "2 words"
str, err := fmt.Sprintln("2 words") // returns string "2 words\n"
str, err := fmt.Sprintf("%v %s", 2, "words") // returns string "2 words"
```

* Fprint、Fprintln、Fprintf

```go
byteCount, err := fmt.Sprint(w, "Hello World") // writes to io.Writer w
```



#### Scan

从标准输入中获取文本

```go
var s string
fmt.Scanln(&s) // pass pointer to buffer
// Scanln is similar to fmt.Scan(), but it stops scanning at new line.
fmt.Println(s) // whatever was inputted
```

#### Stringer接口

fmt.Stringer接口由一个 `String()string` 函数组成

```go
type Stringer interface{
	String() string
}
```

如果在某一类型上定义String()方法，将类型各个字段格式化为一字符串，类似Java中的toString()

```go
type Person struct{
    Name string
    Age int
}

// String satisfies the fmt.Stringer interface
// Defining it on type Person makes it available on *Person as well
func (p Person) String() string {
    return fmt.Sprintf("name=%s age=%s", p.Name, p.Age)
}
```

