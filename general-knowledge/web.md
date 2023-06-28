# Web

## Spring

### IoC



### AOP

<figure><img src="../.gitbook/assets/aop.png" alt=""><figcaption></figcaption></figure>

### BeanFactory & ApplicationContext

| BeanFactory             | ApplicationContext                    |
| ----------------------- | ------------------------------------- |
| 最底层接口，IoC核心             | BeanFactory的子接口                       |
| 延迟加载，getBean才会发现可能的配置问题 | 容器启动时一次性创建所有bean，占用内存空间，启动较慢，运行时速度较快。 |
| 需要显式配置依赖关系              | @Autowaired自动装配                       |
| 不主动管理bean生命周期           | 主动管理                                  |
