## 坑与建议

### 1.sync.WaitGroup陷阱 
```golang
func father(wg *sync.WaitGroup) {
	wg.Add(1)
	defer wg.Done()

	fmt.Printf("father\n")
	for i := 0; i < 10; i++ {
		go child(wg, i)
	}
}

func child(wg *sync.WaitGroup, id int) {
	wg.Add(1)
	defer wg.Done()

	fmt.Printf("child [%d]\n", id)
}

func main() {
	var wg sync.WaitGroup
	go father(&wg)

	wg.Wait()
	log.Printf("main: father and all chindren exit")
}
```

现问题了吗？如果没有看下面的运行结果：main函数在子协程结束前就开始结束了。
```
father
main: father and all chindren exit
child [9]
child [0]
child [4]
child [7]
child [8]
```

产生以上问题的原因在于，创建协程后在协程内才执行Add()函数，而此时Wait()函数可能已经在执行，甚至Wait()函数在所有Add()执行前就执行了，
Wait()执行时立马就满足了WaitGroup的计数器为0，Wait结束，主程序退出，导致所有子协程还没完全退出，main函数就结束了。
#### 正确操作:
Add函数一定要在Wait函数执行前执行
``` golang
for i := 0; i < 10; i++ {
		wg.Add(1)
		go child(wg, i)
}
```
