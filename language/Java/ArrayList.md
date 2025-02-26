## 基础概念

ArrayList是Java集合框架中的一个类，用于动态存储对象
## 使用方法

``` java
/**
 * @program: Backend-Arsenal/Java-Core
 * @description: 实现精简版ArrayList（重点：System.arraycopy优化思路）
 * @author: Selina_Xie
 * @create: 2025-02-25
 */
public class SimpleArrayList<T> {
    private T[] elements;
    private int size;
    private static final int DEFAULT_CAPACITY = 10;

    public SimpleArrayList() {
        elements = (T[]) new Object[DEFAULT_CAPACITY];
    }

    // 实现add方法：向列表中添加元素。如果数组已满，需要进行扩容操作
    public void add(T element) {
        if (size == elements.length) {
            // 扩容操作
            T[] newElments = (T[]) new Object[elements.length * 2];
            System.arraycopy(elements, 0, newElments, 0, elements.length);
            elements = newElments;
        }
        elements[size++] = element;
    }

    // 实现get方法：实现获取指定索引位置元素的方法，记得检查索引是否越界
    public T get(int index) {
        if (index < 0 || index >= size) {
            throw new IndexOutOfBoundsException("Index:" + index + ", Size:" + size);
        }
        return elements[index];
    }

    // 实现size方法：返回当前列表中存储的元素数量
    public int size() {
        return size;
    }

    // 实现remove方法：移除指定索引位置元素的方法。移除元素后，需要将后面的元素向前移动
    public void remove(int index) {
        if (index < 0 || index >= size) {
            throw new IndexOutOfBoundsException("Index:" + index + ", Size:" + size);
        }
        int numMoved = size - index - 1;
        if (numMoved > 0) {
            System.arraycopy(elements, index + 1, elements, index, numMoved);
        }
        elements[--size] = null; // 帮助回收垃圾
    }
}

```
## 底层原理
基于数组实现
- 扩容机制
- System.arraycopy

## 与其他集合对比
- LinkedList