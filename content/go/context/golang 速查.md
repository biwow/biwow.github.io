# golang 速查
## 操作符
&被称为取址操作符；*被称为取值操作符
## 常用技巧
```
<-make(chan struct{}) // hang foreve
```
## 数据类型
整型数 | 范围
:-:|---
int8 | -128 ~ 127
int16 | -32768 ~ 32767
int32 | -2147483648 ~ 2147483647
int64 | -9223372036854775808 ~ 9223372036854775807
uint8 | 0 ~ 256
uint16 | 0 ~ 65535
uint32 | 0 ~ 4294967295
uint64 | 0 ~ 18446744073709551615

## 数据定义
##### 定义map
```
/* 声明变量，默认 map 是 nil */
var map_variable map[key_data_type]value_data_type

/* 使用 make 函数 */
map_variable := make(map[key_data_type]value_data_type)
```
##### 定义切片
```
/* 声明一个未指定大小的数组来定义切片 */
var identifier []type

/* 使用make()函数来创建切片*/
var slice1 []type = make([]type, len)
slice1 := make([]type, len)
```
## 类型转换
##### 字符串转int
```
strconv.Atoi(a)
```
##### 字符串转int
```
strconv.ParseInt(str,10,64)
```
##### int转字符串
```
strconv.Itoa(c)
```
##### int转int64
```
int64(i)
```
## 时间
##### 毫秒级时间戳
```
time.Now().UnixNano() / 1e6
```
##### 秒级时间戳
```
time.Now().Unix()
```

## 反射
##### reflect.Type
```
t := reflect.TypeOf(3)   // a reflect.Type
fmt.Println(t.String())  // "int"
fmt.Println(t)           // "int"
```
##### reflect.Value
```
v := reflect.ValueOf(3) // a reflect.Value
fmt.Println(v) // "3"
fmt.Printf("%v\n", v) // "3"
fmt.Println(v.String()) // NOTE: "<int Value>"

t := v.Type() // a reflect.Type
fmt.Println(t.String()) // "int"

v := reflect.ValueOf(3) // a reflect.Value
x := v.Interface() // an interface{}
i := x.(int) // an int
fmt.Printf("%d\n", i) // "3"
```
##### Elem 解引用
```
x := 2 // value type variable?
a := reflect.ValueOf(2) // 2 int no
b := reflect.ValueOf(x) // 2 int no
c := reflect.ValueOf(&x) // &x *int no
d := c.Elem() // 2 int yes (x)
```
##### Addr 解引用
每当我们通过指针间接地获取的reflect.Value都是可取地址的，即使开始的是一个不可取地址的Value。在反射机制中，所有关于是否支持取地址的规则都是类似的。例如，slice的索引表达式e[i]将隐式地包含一个指针，它就是可取地址的，即使开始的e表达式不支持也没有关系。以此类推，reflect.ValueOf(e).Index(i)对于的值也是可取地址的，即使原始的reflect.ValueOf(e)不支持也没有关系。
要从变量对应的可取地址的reflect.Value来访问变量需要三个步骤。第一步是调用Addr()方
法，它返回一个Value，里面保存了指向变量的指针。然后是在Value上调用Interface()方法，也就是返回一个interface{}，里面通用包含指向变量的指针。最后，如果我们知道变量的类型，我们可以使用类型的断言机制将得到的interface{}类型的接口强制环为普通的类型指针。这样我们就可以通过这个普通指针来更新变量了：
```
x := 2
d := reflect.ValueOf(&x).Elem() // d refers to the variable x
px := d.Addr().Interface().(*int) // px := &x
*px = 3 // x = 3
fmt.Println(x) // "3"
```
或者，不使用指针，而是通过调用可取地址的reflect.Value的reflect.Value.Set方法来更新对于的值：
```
d.Set(reflect.ValueOf(4))
fmt.Println(x) // "4"
```
有很多用于基本数据类型的Set方法：SetInt、SetUint、SetString和SetFloat等
```
d := reflect.ValueOf(&x).Elem()
d.SetInt(3)
fmt.Println(x) // "3"
```

## 字符串
##### 常用处理
```
fmt.Println("查找子串是否在指定的字符串中")
fmt.Println(" Contains 函数的用法")
fmt.Println(strings.Contains("seafood", "foo")) //true
fmt.Println(strings.Contains("seafood", "bar")) //false
fmt.Println(strings.Contains("seafood", ""))    //true
fmt.Println(strings.Contains("", ""))           //true 这里要特别注意
fmt.Println(strings.Contains("我是中国人", "我"))     //true
fmt.Println("")
fmt.Println(" ContainsAny 函数的用法")
fmt.Println(strings.ContainsAny("team", "i"))        // false
fmt.Println(strings.ContainsAny("failure", "u & i")) // true
fmt.Println(strings.ContainsAny("foo", ""))          // false
fmt.Println(strings.ContainsAny("", ""))             // false
fmt.Println("")
fmt.Println(" ContainsRune 函数的用法")
fmt.Println(strings.ContainsRune("我是中国", '我')) // true 注意第二个参数，用的是字符
fmt.Println("")
fmt.Println(" Count 函数的用法")
fmt.Println(strings.Count("cheese", "e")) // 3
fmt.Println(strings.Count("five", ""))    // before & after each rune result: 5 , 源码中有实现
fmt.Println("")
fmt.Println(" EqualFold 函数的用法")
fmt.Println(strings.EqualFold("Go", "go")) //大小写忽略
fmt.Println("")
fmt.Println(" Fields 函数的用法")
fmt.Println("Fields are: %q", strings.Fields("  foo bar  baz   ")) //["foo" "bar" "baz"] 返回一个列表
//相当于用函数做为参数，支持匿名函数
for _, record := range []string{" aaa*1892*122", "aaa\taa\t", "124|939|22"} {
	fmt.Println(strings.FieldsFunc(record, func(ch rune) bool {
		switch {
		case ch > '5':
			return true
		}
		return false
	}))
}
fmt.Println("")
fmt.Println(" HasPrefix 函数的用法")
fmt.Println(strings.HasPrefix("NLT_abc", "NLT")) //前缀是以NLT开头的
fmt.Println("")
fmt.Println(" HasSuffix 函数的用法")
fmt.Println(strings.HasSuffix("NLT_abc", "abc")) //后缀是以NLT开头的
fmt.Println("")
fmt.Println(" Index 函数的用法")
fmt.Println(strings.Index("NLT_abc", "abc")) // 返回第一个匹配字符的位置，这里是4
fmt.Println(strings.Index("NLT_abc", "aaa")) // 在存在返回 -1
fmt.Println(strings.Index("我是中国人", "中"))     // 在存在返回 6
fmt.Println("")
fmt.Println(" IndexAny 函数的用法")
fmt.Println(strings.IndexAny("我是中国人", "中")) // 在存在返回 6
fmt.Println(strings.IndexAny("我是中国人", "和")) // 在存在返回 -1
fmt.Println("")
fmt.Println(" Index 函数的用法")
fmt.Println(strings.IndexRune("NLT_abc", 'b')) // 返回第一个匹配字符的位置，这里是4
fmt.Println(strings.IndexRune("NLT_abc", 's')) // 在存在返回 -1
fmt.Println(strings.IndexRune("我是中国人", '中'))   // 在存在返回 6
fmt.Println("")
fmt.Println(" Join 函数的用法")
s := []string{"foo", "bar", "baz"}
fmt.Println(strings.Join(s, ", ")) // 返回字符串：foo, bar, baz
fmt.Println("")
fmt.Println(" LastIndex 函数的用法")
fmt.Println(strings.LastIndex("go gopher", "go")) // 3
fmt.Println("")
fmt.Println(" LastIndexAny 函数的用法")
fmt.Println(strings.LastIndexAny("go gopher", "go")) // 4
fmt.Println(strings.LastIndexAny("我是中国人", "中"))      // 6
fmt.Println("")
fmt.Println(" Map 函数的用法")
rot13 := func(r rune) rune {
	switch {
	case r >= 'A' && r <= 'Z':
		return 'A' + (r-'A'+13)%26
	case r >= 'a' && r <= 'z':
		return 'a' + (r-'a'+13)%26
	}
	return r
}
fmt.Println(strings.Map(rot13, "'Twas brillig and the slithy gopher..."))
fmt.Println("")
fmt.Println(" Repeat 函数的用法")
fmt.Println("ba" + strings.Repeat("na", 2)) //banana
fmt.Println("")
fmt.Println(" Replace 函数的用法")
fmt.Println(strings.Replace("oink oink oink", "k", "ky", 2))
fmt.Println(strings.Replace("oink oink oink", "oink", "moo", -1))
fmt.Println("")
fmt.Println(" Split 函数的用法")
fmt.Printf("%q\n", strings.Split("a,b,c", ","))
fmt.Printf("%q\n", strings.Split("a man a plan a canal panama", "a "))
fmt.Printf("%q\n", strings.Split(" xyz ", ""))
fmt.Printf("%q\n", strings.Split("", "Bernardo O'Higgins"))
fmt.Println("")
fmt.Println(" SplitAfter 函数的用法")
fmt.Printf("%q\n", strings.SplitAfter("/home/m_ta/src", "/")) //["/" "home/" "m_ta/" "src"]
fmt.Println("")
fmt.Println(" SplitAfterN 函数的用法")
fmt.Printf("%q\n", strings.SplitAfterN("/home/m_ta/src", "/", 2))  //["/" "home/m_ta/src"]
fmt.Printf("%q\n", strings.SplitAfterN("#home#m_ta#src", "#", -1)) //["/" "home/" "m_ta/" "src"]
fmt.Println("")
fmt.Println(" SplitN 函数的用法")
fmt.Printf("%q\n", strings.SplitN("/home/m_ta/src", "/", 1))
fmt.Printf("%q\n", strings.SplitN("/home/m_ta/src", "/", 2))  //["/" "home/" "m_ta/" "src"]
fmt.Printf("%q\n", strings.SplitN("/home/m_ta/src", "/", -1)) //["" "home" "m_ta" "src"]
fmt.Printf("%q\n", strings.SplitN("home,m_ta,src", ",", 2))   //["/" "home/" "m_ta/" "src"]
fmt.Printf("%q\n", strings.SplitN("#home#m_ta#src", "#", -1)) //["/" "home/" "m_ta/" "src"]
fmt.Println("")
fmt.Println(" Title 函数的用法") //这个函数，还真不知道有什么用
fmt.Println(strings.Title("her royal highness"))
fmt.Println("")
fmt.Println(" ToLower 函数的用法")
fmt.Println(strings.ToLower("Gopher")) //gopher
fmt.Println("")
fmt.Println(" ToLowerSpecial 函数的用法")
fmt.Println("")
fmt.Println(" ToTitle 函数的用法")
fmt.Println(strings.ToTitle("loud noises"))
fmt.Println(strings.ToTitle("loud 中国"))
fmt.Println("")
fmt.Println(" Replace 函数的用法")
fmt.Println(strings.Replace("ABAACEDF", "A", "a", 2)) // aBaACEDF
//第四个参数小于0，表示所有的都替换， 可以看下golang的文档
fmt.Println(strings.Replace("ABAACEDF", "A", "a", -1)) // aBaaCEDF
fmt.Println("")
fmt.Println(" ToUpper 函数的用法")
fmt.Println(strings.ToUpper("Gopher")) //GOPHER
fmt.Println("")
fmt.Println(" Trim  函数的用法")
fmt.Printf("[%q]", strings.Trim(" !!! Achtung !!! ", "! ")) // ["Achtung"]
fmt.Println("")
fmt.Println(" TrimLeft 函数的用法")
fmt.Printf("[%q]", strings.TrimLeft(" !!! Achtung !!! ", "! ")) // ["Achtung !!! "]
fmt.Println("")
fmt.Println(" TrimSpace 函数的用法")
fmt.Println(strings.TrimSpace(" \t\n a lone gopher \n\t\r\n")) // a lone gopher
```
