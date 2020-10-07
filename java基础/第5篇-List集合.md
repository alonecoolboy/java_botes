## list

collection有两个子类： java.util.List 集合、 java.util.Set 集合

**list接口介绍**

在List集合中允许出现重复的元素，所有的元素是以一种线性方式进行存储的，在程序中可以通过
索引来访问集合中的指定元素。另外，List集合还有一个特点就是元素有序，即元素的存入顺序和取出顺序一致。

注意：ArrayList是list的一个子类

list接口的常用方法：：

List作为Collection集合的子接口，不但继承了Collection接口中的全部方法，而且还增加了一些根据元素索引来操
作集合的特有方法，如下：

+ public void add(int index, E element) : 将指定的元素，添加到该集合中的指定位置上。
+ public E get(int index) :返回集合中指定位置的元素。
+ public E remove(int index) : 移除列表中指定位置的元素, 返回的是被移除的元素。
+ public E set(int index, E element) :用指定元素替换集合中指定位置的元素,返回值的更新前的元素。

**List的子类**

**ArrayList集合**

java.util.ArrayList 集合数据存储的结构是**数组结构**。元素增删慢，查找快，由于日常开发中使用最多的功能为
查询数据、遍历数据，所以 ArrayList 是最常用的集合。

**LinkedList集合**

java.util.LinkedList 集合数据存储的结构是链表结构（双向链表）。方便元素添加、删除的集合

LinkedList提供了大量首尾操作的方法。这些方法我们作为了解即可：

+ public void addFirst(E e) :将指定元素插入此列表的开头。
+ public void addLast(E e) :将指定元素添加到此列表的结尾。
+ public E getFirst() :返回此列表的第一个元素。
+ public E getLast() :返回此列表的最后一个元素。
+ public E removeFirst() :移除并返回此列表的第一个元素。
+ public E removeLast() :移除并返回此列表的最后一个元素。
+ public E pop() :从此列表所表示的堆栈处弹出一个元素。
+ public void push(E e) :将元素推入此列表所表示的堆栈。
+ public boolean isEmpty() ：如果列表不包含元素，则返回true。

LinkedList是List的子类，List中的方法LinkedList都是可以使用，

**set接口**

它与 Collection 接口中的方法基本一致，并没有对 Collection 接口进行功能上的扩充，只是比 Collection 接口更加严格了。与 List 接口不同的是， Set 接口中元素无序，并且都会以某种规则保证存入的元素不出现重复。

Set 集合有多个子类，这里我们介绍其中的 java.util.**HashSet** 、 java.util.**LinkedHashSet** 这两个集合。

java.util.HashSet 是 Set 接口的一个实现类，它所存储的元素是**不可重复**的，并且元素都是**无序**的(即存取顺序不一致)。 java.util.**HashSet 底层的实现**其实是一个 java.util.**HashMap** 支持。
HashSet 是根据**对象的哈希值**来确定元素在集合中的存储位置，因此具有良好的存取和查找性能。保证元素唯一性的方式依赖于： **hashCode 与 equals** 方法。

**HashSet集合存储数据的结构（哈希表）**

在JDK1.8之前，哈希表底层采用**数组+链表**实现，即使用**链表处理冲突**，同一hash值的链表都存储在一个链表里。但是当位于一个桶中的元素较多，即hash值相等的元素较多时，**通过key值依次查找的效率较低**。而JDK1.8中，哈希表存储采用**数组+链表+红黑树**实现，当链表长度超过阈值（8）时，将链表转换为**红黑树**，这样大大减少了查找时间。

![image-20200924121313023](https://i.loli.net/2020/10/07/87Wp42jmYTNUgXA.png)

引入红黑树大程度优化了HashMap的性能，那么对于我们来讲保证HashSet集合元素的唯一，其实就是根据对象的hashCode和equals方法来决定的。如果我们往集合中存放自定义的对象，那么保证其唯一，就必须复写hashCode和equals方法建立属于当前对象的比较方式。

**HashSet存储自定义类型元素**

给HashSet中存放自定义类型元素时，需要重写对象中的hashCode和equals方法，建立自己的比较方式，才能保证HashSet集合中的对象唯一

自定义student类：

如果要用hashset存储自定义student类，I在student类中重写hashcode和equal方法，这样才能在set中判断是否重复

```java
 @Override
    public boolean equals(Object o) {
        if (this == o)
            return true;
        if (o == null || getClass() != o.getClass())
            return false;
        Student student = (Student) o;
        return age == student.age &&
               Objects.equals(name, student.name);
    }
    @Override
    public int hashCode() {
        return Objects.hash(name, age);//重写hashcode方法，往函数传入类属性
    }
}
```

**LinkedHashSet**

HashSet保证元素唯一，可是元素存放进去是没有顺序的，那么我们要保证有序，怎么办呢？在HashSet下面有一个子类 java.util.LinkedHashSet ，它是链表和哈希表组合的一个数据存储结构。



**可变参数**

JDK1.5，定义一个方法需要接受多个参数，并且多个参数类型一致，我们可以对其简化成如下格式：

```java
 public static int getSum(int... arr) {
        int sum = 0;
        for (int a : arr) {
            sum += a;
        }
        return sum;
    }
```

