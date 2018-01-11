
```
func syncAfter() {
    let time: TimeInterval = 2.0
    print(Date())//2018-01-09 08:20:48 +0000
    DispatchQueue.main.asyncAfter(deadline: .now() + time) {
        print(Date())//2018-01-09 08:20:54 +0000
        print("2秒后输出2in\(Thread.current)")//2秒后输出2in<NSThread: 0x608000264800>{number = 1, name = main}
    }
    print(Date())//2018-01-09 08:20:48 +0000
    for i in 0...1000000 {
        //大约6s
        print(i*i*i)
    }
    print(Date())//2018-01-09 08:20:54 +0000
}
```
> 主队列异步执行延时操作，不会开启新线程，顺序执行，等到后面的耗时操作执行完毕之后才会执行延时任务。也就是说在延时操作之后若有耗时操作，那么延时的时长会不准确


```
func asyncAfter() {
    let time: TimeInterval = 2.0
    print(Date())//2018-01-11 09:10:24 +0000
    DispatchQueue.global().asyncAfter(deadline: .now() + time) {
        print(Date())//2018-01-11 09:10:26 +0000
        print("2秒后输出2in\(Thread.current),\(Date())")//2秒后输出2in<NSThread: 0x60400026f000>{number = 5, name = (null)},2018-01-11 09:10:26 +0000
    }
    print(Date())//2018-01-11 09:10:24 +0000
    for i in 0...500000 {
        //大约6s
        print("\(i),\(Date())")
    }
    print(Date())//2018-01-11 09:10:31 +0000
}
```
> 全局队列异步执行延时操作，开启新线程，会在准确的延时时长执行操作，但**此时是在子线程执行**。

