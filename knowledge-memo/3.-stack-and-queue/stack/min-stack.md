# min stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

{% tabs %}
{% tab title="Notes" %}
* one stack with maintaining min&#x20;
* two stacks
{% endtab %}

{% tab title="Solution" %}
```java
//one stack
class MinStack {
    public int min;
    public Stack<Integer> stack;
    
    public MinStack() {
        min = Integer.MAX_VALUE;
        stack = new Stack();
    }
    
    public void push(int x) {
        if (x <= min) { // <= !!! push the old min before push a new min
            stack.push(min);
            min = x;
        }
        
        stack.push(x);
    }
    
    public void pop() {
        if (stack.size() == 0) {
            return;
        }
        
        if (min == stack.pop()) { // back to an old min
            min = stack.pop();
        }
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return min;
    }
}

//two stacks
public class MinStack {
    private Stack<Integer> stack;
    private Stack<Integer> minStack;

    public MinStack() {
        stack = new Stack<Integer>();
        minStack = new Stack<Integer>();
    }

    public void push(int number) {
        stack.push(number);
        if (minStack.empty() == true || minStack.peek() >= number) {
            minStack.push(number);
        }
    }

    public int pop() {
        if (stack.peek().equals(minStack.peek()) ) // equals!!! Integer object
            minStack.pop();
        return stack.pop();
    }

    public int min() {
        return minStack.peek();
    }
}
```
{% endtab %}
{% endtabs %}
