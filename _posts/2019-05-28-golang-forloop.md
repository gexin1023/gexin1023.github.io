---
layout: post
title: 多个goroutine共享变量时的两种错误用法
toc: true
---

* 
{:toc}

## 闭包中直接使用循环体中变化的量

platground链接：

[https://play.golang.org/p/6x6_tuQNjUO](https://play.golang.org/p/6x6_tuQNjUO)

```golang
type Value struct{
	val int
}

func (v *Value)print(){
	time.Sleep(time.Second)
	fmt.Println(v.val)
}

func main() {
	vals := make([]Value,0)

	for  i := 0; i <5;i++ {
		vals = append(vals, Value{val:i,})
	}

	for _,v := range vals{
		// 这种形式，闭包方式共享了主协程的变量v
		// 而变量v是不断变化的，所以导致print的值都是最后一个
		go func(){
		   v.print()	
		}()
	}

	time.Sleep(time.Second*3)
}

```

```
运行结果：
4
4
4
4
4
```

正确用法应该是在闭包的参数中将变量作为参数传递

```golang
for _,v := range vals{
	go func(v Value){
		v.print()	
	}(v)
}
```


## receiver为指针时候，创建goroutine

playground链接：
[https://play.golang.org/p/6quZIn6ZwSM](https://play.golang.org/p/6quZIn6ZwSM)

```golang
type Value struct{
	val int
}

func (v *Value)print(){
	time.Sleep(time.Second)
	fmt.Println(v.val)
}

func main() {

	vals := make([]Value,0)

	for  i := 0; i <5;i++ {
		vals = append(vals, Value{val:i,})
	}

	for _,v := range vals{
		// print方法的receiver是（*Value）类型，而此处v是一个Value类型
		// 所以每次print传值都传递了&v。
		// 在for loop中，v的值变化，但是&v不会改变
		// 在其他goroutine中执行时，print的内容不可预期，取决于当时的v值
		go v.print()
	}

	time.Sleep(time.Second*3)
}
```

```
运行结果：
4
4
4
4
4
```

如果非要使用这种方式在迭代中使用goroutine，可以采用如下三种方式修改

1. 可以将print方法的接受者改为实体类型，而非引用。这样每次Goroutine都是以值复制的形式传入，实现迭代。

```golang
func (v Value)print(){
	time.Sleep(time.Second)
	fmt.Println(v.val)
}
```

2. 也可以声明一个临时变量，用于保存v值

```golang
for _,v := range vals{
	tmp := v
	go tmp.print()
}
```

3. 也可以将v的类型改为引用类型

```
func main() {

	vals := make([]*Value,0)

	for  i := 0; i <5;i++ {
		vals = append(vals, &Value{val:i,})
	}

	for _,v := range vals{
		go v.print()
	}

	time.Sleep(time.Second*3)
}
```
