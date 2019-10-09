---
layout: post
title: golang pprof工具使用及参数解读
toc: true
---

* 
{:toc}

## pprof使用

pprof工具使用可以使用`net/http/pprof`或者是`runtime/pprof`实现，这两个包实现的功能基本一致，只是前者提供了http方式的访问(个人更习惯使用`net/http/pprof`)。

pprof提供如下几种功能:

* **allocs**: A sampling of all past memory allocations
* **block**: Stack traces that led to blocking on synchronization primitives
* **cmdline**: The command line invocation of the current program
* **goroutine**: Stack traces of all current goroutines
* **heap**: A sampling of memory allocations of live objects. You can specify the gc GET parameter to run GC before taking the heap sample.
* **mutex**: Stack traces of holders of contended mutexes
* **profile**: CPU profile. You can specify the duration in the seconds GET parameter. After you get the profile file, use the go tool pprof command to investigate the profile.
* **threadcreate**: Stack traces that led to the creation of new OS threads
* **trace**: A trace of execution of the current program. You can specify the duration in the seconds GET parameter. After you get the trace file, use the go tool trace command to investigate the trace.

### net/http/pprof

使用方式很简单，在自己程序中引入`"net/http/pprof"`，然后http监听`"0.0.0.0:6060"`就可以了。

```golang
package main

import (
	"fmt"
	"github.com/ethereum/go-ethereum/crypto"
	"net/http"
	_ "net/http/pprof"
	"time"
)

func main() {
	go func() {
		for {
			t := time.Now().String()
			h := crypto.Keccak256([]byte(t))
			fmt.Println(h)
			time.Sleep(time.Millisecond)
		}
	}()

	http.ListenAndServe("0.0.0.0:6060", nil)
}
```

使用pprof工具就可以对运行中的程序进行profile了，cpu profiling的使用方式如下所示。

```shell
# 默认采样时间30秒
go tool pprof http://127.0.0.1:6060/debug/pprof/profile

# 指定采样时间10秒
go tool pprof http://127.0.0.1:6060/debug/pprof/profile?seconds=10

# 生成可视化pdf
go tool pprof -pdf http://127.0.0.1:6060/debug/pprof/profile?seconds=10

# 生成可视化svg
go tool pprof -svg http://127.0.0.1:6060/debug/pprof/profile?seconds=10
```

也可以使用浏览器浏览信息 http://127.0.0.1:6060/debug/pprof/

同样的，假如需要对于memory进行分析，只需将上面代码块中的`profile`改成`allocs`就可以了。

## 参数解读

```
flat	flat%	sum%	cum	    cum%	
11.12s	20.23%	20.23%	11.50s	20.92%	syscall.Syscall
5.84s	10.63%	30.86%	5.84s	10.63%	runtime.pcvalue
1.73s	3.15%	34.01%	1.73s	3.15%	runtime.futex
1.69s	3.07%	37.08%	7.21s	13.12%	runtime.mallocgc
```

* flat: 统计周期内的执行时间
* flat%: 执行时间占比
* cum: 统计周期内的执行时间（包括子调用）
* cum%: 执行占比（包括子调用）



