# 并发

### Process Thread Coroutine

![](../../.gitbook/assets/协程.jpeg)

* 一个进程可以拥有一个或者多个线程，线程只存在于一个进程里。
* 进程有自己的地址空间，占据独立内存，资源共享复杂，切换开销大，同步简单；线程间资源共享容易，同步需要加锁。
* 协程是一种用户态的轻量级线程，保留上一次调用状态，无需上下文切换开销。
* 线程协程适合IO密集型应用，多进程适合CPU计算密集型应用以利用多核。

### 乐观锁和悲观锁

* 乐观锁：不上锁，更新时检查数据是否被修改过，修改过则放弃操作
  * Compare And Swap(CAS)：VAB，如果内存位置V的值等于预期值A，则位置更新为新值B，否则不执行操作，自旋（重试至成功）；限制：单个变量原子性，ABA问题（即修改为原来的数据，栈顶问题，可加版本号解决）
  * 版本号：修改version++，更新时version?=读取时version
* 悲观锁：总加锁，block其他线程

适用于不同场景，如乐观锁适合多读应用类型以提高吞吐量，避免使用于并发冲突概率高的场景下一直重试导致CPU开销较大

{% embed url="https://www.cnblogs.com/kismetv/p/10787228.html" %}

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
| less flexible as language-level construct | more flexible, e.g. Condition variables             |

### synchronized底层实现

JVM会找到对象的monitor，如果成功加锁就称为该monitor的唯一持有者，monitor在被释放前不能再被其它线程获取。

synchronized在编译后会产生monitorenter和monitorexit字节码指令，并需要一个引用类型的参数指明要锁定和解锁的对象，i.e.

* 同步实例方法：实例对象
* 同步静态方法：Class对象
* 同步方法块：括号里的对象

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
