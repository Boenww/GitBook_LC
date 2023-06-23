# 并发

### volatile作用

* 保证可见行：读取前从主内存中刷新，写入后立即同步回主内存。
* 防止指令重排
* 不保证原子性：e.g. 两个线程各自执行count++，可能导致最终count结果为1，不是预期的2

### 线程间通信协作方式

* volatile
* wait/notify
* join
* ThreadLocal: e.g. 主线程threadLocal.set, 子线程threadLocal.get

### synchronized vs ReentrantLock

| synchronized                              | ReentrantLock                                       |
| ----------------------------------------- | --------------------------------------------------- |
| implicit lock                             | explicit lock, i.e. need lock and unlock manually   |
| 等待锁时不可中断                                  | 可通过lockInterruptibly()在等待获取锁时，响应中断，i.e. interrupt() |
| unfair lock                               | unfair lock by default, fair lock by constructor    |
| less flexible as language-level construct | more flexible, e.g. condition variables             |

### CountDownLatch vs CyclicBarrier

* CDL: 计数器，可以调整线程之间的执行顺序

```
CountDownLatch down = new CountDownLatch(1);
down.await();        // 线程挂起，等待count值为0时才继续执行
down.countDown();    // count - 1
down.getCount();
```

* CB: 允许多个线程相互等待，等达到一个共同点后再继续执行，e.g. 计算数据最后合并计算结果。

### 银行家算法

要求进程在申请资源之前必须先声明它所需要的最大资源数，需要进程请求资源时，检查请求是否<=系统当前可用的资源数，并模拟分配资源给进程，通过安全性算法检查系统是否仍然处于安全状态，如果不安全，分配将被推迟。

### 如何尽量避免死锁

* 减小锁范围
* 按一定顺序申请锁
* 非阻塞锁，e.g. tryLock()
