# Nginx

## select/poll vs. epoll

select/poll: 线性存储socket集合，O(n)，用户态和内核态之间的拷贝（集合拷贝到内核->内核遍历标记可读或可写->拷贝回用户态->用户态遍历找到标记并处理）

epoll: 内核维护了红黑树存储待检测socket，增删改O(logn)，维护了链表来记录就绪事件，通过事件驱动传递给应用程序；解决C10K(Client 1万请求)





## 惊群效应









