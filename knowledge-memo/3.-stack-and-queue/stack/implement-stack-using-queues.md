# 225. implement stack using queues

{% tabs %}
{% tab title="Notes" %}
* two queues
* one queue
{% endtab %}

{% tab title="Solution" %}
```java
class MyStack {
    public Queue<Integer> queue1;
    public Queue<Integer> queue2;
    
    /** Initialize your data structure here. */
    public MyStack() {
        queue1 = new LinkedList<>();
        queue2 = new LinkedList<>();
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        queue1.offer(x);
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        while (queue1.size() != 1) {
            queue2.offer(queue1.poll());
        }
        
        int res = queue1.poll();
        Queue<Integer> tmp = queue1;
        queue1 = queue2;
        queue2 = tmp;
        return res;
    }
    
    /** Get the top element. */
    public int top() {
        while (queue1.size() != 1) {
            queue2.offer(queue1.poll());
        }
        
        int res = queue1.poll();
        Queue<Integer> tmp = queue1;
        queue1 = queue2;
        queue2 = tmp;
        queue1.offer(res);
        
        return res;
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return queue1.isEmpty();
    }
}

//one queue
class MyStack {
    public Queue<Integer> queue;
    
    /** Initialize your data structure here. */
    public MyStack() {
        queue = new LinkedList<>();
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        queue.offer(x);
        reverse(queue);
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        return queue.poll();
    }
    
    /** Get the top element. */
    public int top() {
        return queue.peek();
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return queue.isEmpty();
    }

    public void reverse(Queue<Integer> queue) {
        int size = queue.size();
        while (size > 1) {
            queue.offer(queue.poll());
            size--;
        }
    }
}
```
{% endtab %}
{% endtabs %}

