## Map集合

![image-20200924125802378](https://i.loli.net/2020/10/10/hobJO4Qy73Pm6xT.png)

Collection 中的集合，元素是孤立存在的（理解为单身），向集合中存储元素采用一个个元素的方式存储。
Map 中的集合，元素是成对存在的(理解为夫妻)。每个元素由键与值两部分组成，通过键可以找对所对应的
值。
Collection 中的集合称为单列集合， Map 中的集合称为双列集合。
需要注意的是， Map 中的集合不能包含重复的键，值可以重复；每个键只能对应一个值。

**Map的子类**

Map有多个子类，这里我们主要讲解常用的**HashMap**集合、**LinkedHashMap**集合

+ HashMap ：存储数据采用的哈希表结构，元素的存取顺序不能保证一致。由于要保证键的唯一、不重复，需要重写键的hashCode()方法、equals()方法
+ LinkedHashMap ：HashMap下有个子类LinkedHashMap，存储数据采用的哈希表结构+链表结构。通过链表结构可以保证元素的存取顺序一致；通过哈希表结构可以保证的键的唯一、不重复，需要重写键的hashCode()方法、equals()方法。

Map接口常用方法：

+ public V put(K key, V value) : 把指定的键与指定的值添加到Map集合中。
+ public V remove(Object key) : 把指定的键 所对应的键值对元素 在Map集合中删除，返回被删除元素的值。
+ public V get(Object key) 根据指定的键，在Map集合中获取对应的值。
+ public Set<K> keySet() : 获取Map集合中所有的键，存储到Set集合中。
+ public Set<Map.Entry<K,V>> entrySet() : 获取到Map集合中所有的键值对对象的集合(Set集合)。

**注意：**

使用**put方法**时，若指定的键**(key)在集合中没有**，则**没有这个键对应的值**，返回null，并把指定的键值添加到集合中；
若指定的键(key)在集合中存在，则返回值为集合中键对应的值（**该值为替换前的值**），并把指定键所对应的值，替换成指定的新值。

**Map 集合遍历键找值方式**

```java
Set<String> keys = map.keySet();
        // 遍历键集 得到 每一个键
        for (String key : keys) {
           //key  就是键  
            //获取对应值
            String value = map.get(key);
            System.out.println(key+"的CP是："+value);
        } 
```

**Entry 键值对对象**

Map 中存放的是两种对象，一种称为key(键)，一种称为value(值)，它们在在 Map 中是一一对应关系，这一对对象又称做 Map 中的一个 Entry( 项) 。 Entry 将键值对的对应关系封装成了对象。即键值对对象，这样我们在遍历 Map 集合时，就可以从每一个键值对（ Entry ）对象中获取对应的键与对应的值。

既然Entry表示了一对键和值，那么也同样提供了获取对应键和对应值得方法：
public K getKey() ：获取Entry对象中的键。
public V getValue() ：获取Entry对象中的值。

在Map集合中也提供了获取所有Entry对象的方法：
public Set<Map.Entry<K,V>> entrySet() : 获取到Map集合中所有的键值对对象的集合(Set集合)。

**Map 集合遍历键值对方式**

```java
// 获取 所有的 entry对象  entrySet
        Set<Entry<String,String>> entrySet = map.entrySet();
        // 遍历得到每一个entry对象
        for (Entry<String, String> entry : entrySet) {
           // 解析  
            String key = entry.getKey();
            String value = entry.getValue(); 
            System.out.println(key+"的CP是:"+value);
        }
```

HashMap 存储自定义类型键值

当给 HashMap中存放自定义对象时，如果自定义对象作为key存在，这时要保证对象唯一，必须复写对象的hashCode和equals方法(如果忘记，请回顾HashSet存放自定义对象)。
如果要保证 map中存放的key和取出的顺序一致，可以使用 java.util.LinkedHashMap 集合来存放。

**LinkedHashMap**

放入元素是有顺序的

```java
LinkedHashMap<String, String> map = new LinkedHashMap<String, String>();
```

JDK9集合添加的优化：

通常，我们在代码中创建一个集合（例如，List 或 Set ），并直接用一些元素填充它。 实例化集合，几个 add方法调用，使得代码重复

Java 9，添加了几种集合工厂方法,更方便创建少量元素的集合、map实例。新的List、Set、Map的静态工厂方法可
以更方便地创建集合的不可变实例。

```java
public class HelloJDK9 { 
    public static void main(String[] args) { 
        Set<String> str1=Set.of("a","b","c");//这样的方式创建的是不可变的实例 
        //str1.add("c");这里编译的时候不会错，但是执行的时候会报错，因为是不可变的集合 
        System.out.println(str1); 
        Map<String,Integer> str2=Map.of("a",1,"b",2); 
        System.out.println(str2); 
        List<String> str3=List.of("a","b"); 
        System.out.println(str3); 
    } 
}
```

+ of()方法只是Map，List，Set这三个接口的静态方法，其父类接口和子类实现并没有这类方法，比如HashSet，ArrayList等；
+ 返回的集合是不可变的；