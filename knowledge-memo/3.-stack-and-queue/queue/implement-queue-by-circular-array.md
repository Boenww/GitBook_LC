# 622. implement queue by circular array

Implement queue by circular array. You need to support the following methods:

1. `CircularQueue(n):` initialize a circular array with size n to store elements
2. `boolean isFull():` return `true` if the array is full
3. `boolean isEmpty():` return `true` if there is no element in the array
4. `void enqueue(element):` add an element to the queue
5. `int dequeue():` pop an element from the queue

![circular array](http://media.jiuzhang.com/markdown/images/4/4/403995f8-37d6-11e8-ae7b-0242ac110002.jpg)

{% tabs %}
{% tab title="Notes" %}
* 如何实现
  1. 我们需要知道队列的入队操作是只在队尾进行的，相对的出队操作是只在队头进行的，所以需要两个变量front与rear分别来指向队头与队尾
  2. 由于是循环队列，我们在增加元素时，如果此时 rear = array.length - 1 ，rear 需要更新为 0；同理，在元素出队时，如果 front = array.length - 1, front 需要更新为 0. 对此，我们可以通过对数组容量取模来更新。
* size is fixed -&gt; consider edge cases
{% endtab %}

{% tab title="Solution" %}
```java
public class CircularQueue {
    public int[] array;
    public int front, rear, size;
    
    public CircularQueue(int n) {
        array = new int[n];
        size = 0;
        front = 0;
        rear = 0;
    }

    public boolean isFull() {
        return size == array.length;
    }


    public boolean isEmpty() {
        return size == 0;
    }

    public void enqueue(int element) {
        if (isFull()) {
            return false;
        }
        
        array[rear++] = element;
        size++;
        if (rear == array.length) {
            rear = 0;
        }
        
        return true;
        // modulo method
        // rear = (front + size) % array.length;
        // array[rear] = element;
        // size++;
    }

    public int dequeue() { //or boolean
        int res = array[front];
        
        array[front++] = 0;
        size--;
        if (front == array.length) {
            front = 0;
        }
        
        // modulo method
        // front = (front + 1) % array.length;
        // size--;
        return res;
    }
    
    public int Front() {
        if (isEmpty()) {
            return -1;
        }
        
        return array[front];
    }
    
    public int Rear() {
        if (isEmpty()) {
            return -1;
        }
        
        return rear == 0 ? array[array.length - 1] : array[rear - 1];
    }
}
```
{% endtab %}
{% endtabs %}

