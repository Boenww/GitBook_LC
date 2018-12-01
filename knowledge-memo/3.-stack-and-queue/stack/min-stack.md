---
description: >-
  Design a stack that supports push, pop, top, and retrieving the minimum
  element in constant time.
---

# min stack

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
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
```
{% endtab %}
{% endtabs %}

