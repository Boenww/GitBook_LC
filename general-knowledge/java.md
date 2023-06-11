# Java

## JVM

### 组成

* JVM memory
  * 线程私有：Program counter register (byte code where the thread executes and tells the address of the next exec instruction to execution engine), JVM stack, native method stack
  * 线程共享：heap, method area (类信息、常量、静态变量、JIT compiled code等)
* class loader:&#x20;
*

### 作用

compiler -Java cod-> byte code -> class loader加载到内存中 -> execution engine跟native interface交互将byte code翻译为底层系统指令再交由CPU执行

### 类加载过程



### heap & stack

| heap                         | stack                                              |
| ---------------------------- | -------------------------------------------------- |
| 数据存储，stores object instances | 方法执行，stores 局部变量、返回方法地址等                           |
| 不连续、不固定、更大，慢、运行期确认           | 连续、固定、快、编译器确认                                      |
|                              | 每个方法被调用直到执行完成的过程，就对应着一个stack frame在虚拟机栈中从入栈到出栈的过程。 |



### 对象分配如何保证线程安全？

* CAS (Compare and Swap, 3 operands: memory location & expected value & new value, like AtomicInteger)，效率低。
* 线程在堆中预分配内存，一般采用这种策略。





## GC

### 如何判断对象是否可被回收？

* 引用计数：存在循环引用的问题，一般不使用。
* 可达性分析：通过GC Roots作为起始节点，根据引用关系向下搜索，搜索不到就被标记为垃圾。

### 引用类型



### 垃圾回收算法

* copy
* 标记清理
* 标记整理





内存泄漏：长生命周期对象持有短生命周期对象的引用可能导致内存泄漏

## Spring

### AOP



### IoC (DI)

