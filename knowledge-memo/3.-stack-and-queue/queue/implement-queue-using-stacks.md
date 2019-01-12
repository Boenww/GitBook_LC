# implement queue using stacks

Implement the following operations of a queue using stacks.

* push\(x\) -- Push element x to the back of queue.
* pop\(\) -- Removes the element from in front of queue.
* peek\(\) -- Get the front element.
* empty\(\) -- Return whether the queue is empty.

{% tabs %}
{% tab title="Notes" %}
在获取队头元素或者删除队头元素的时候，我们先判断stack1是否为空，如果不为空，从stack1中取即可，如果为空，那么将stack2中的元素倒入到stack1中，每次加入元素的时候都是往stack2中加入元素。
{% endtab %}

{% tab title="Solution" %}
```java
class MyQueue {
    public Stack<Integer> stack1, stack2;
    
    public MyQueue() {
        stack1 = new Stack<>();
        stack2 = new Stack<>();
    }
    
    public void push(int x) {
        stack2.push(x);
    }
    
    public int pop() {
        if (stack1.isEmpty()) {
            stack2ToStack1();
        }
        
        return stack1.pop();
    }
    
    public int peek() {
        if (stack1.isEmpty()) {
            stack2ToStack1();
        }
        
        return stack1.peek();
    }
    
    public boolean empty() {
        return stack1.isEmpty() && stack2.isEmpty();
    }
    
    public void stack2ToStack1() {
        while (!stack2.isEmpty()) {
            stack1.push(stack2.pop());
        }
    }
}
```
{% endtab %}
{% endtabs %}

