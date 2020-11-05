# lombok教程

会利用注解自动生成 java Bean 中烦人的 Getter、Setter，还能自动生成 logger、ToString、HashCode、Builder 等 java特色的函数或是符合设计模式的函数，能够让你 java Bean 更简洁，更美观。

**maven依赖：**

```html
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.16.20</version>
</dependency>
```

**@Getter、@Setter**

加在属性上：对这个属性起作用

加在类上：对整个类的属性起作用

@Getter用于创建属性的getter方法，@Setter用于创建属性的setter方法

`@Setter(AccessLevel.PROTECTED)`可以添加参数，指定权限为私有，默认修饰符public

```java
@Setter
private int age;
```

实际上等价于创建函数（age变成Age）：

```
 public void setAge(int age) {
41         this.age = age;
42     }
```

关于布尔变量的getter

```java
@Getter
private boolean active;
@Getter
private Boolean none;
```

等价于：

```java
 public boolean isActive() {
         return this.active;
     }
 public Boolean getNone() {
         return this.none;
     }
```

基本类型boolean和包装类型Boolean的get函数不一样

**@ToString**

相当于重写了toString函数，通过callSuper参数来指定是否引用父类，includeFieldNames参数设为true，就能明确的输出toString()属性。

```java
@ToString(exclude=”A”)//生成toString的 时候是不包括A属性值
@ToString(exclude={“A″,”B″}//生成toString的时候是不包括A、B属性值
@ToString(of=”A”)//生成toString的时候只包括A属性值
@ToString(of={“B″,”A”})//生成toString的时候只包括A、B属性值
```

**@EqualsAndHashCode**

默认情况下，使用所有非静态和非瞬态（non-transient）属性来生成equals和hasCode。可以通过exclude注解来排除一些属性。

```java
@EqualsAndHashCode(exclude={"a", "b"})//生成equals和hasCode排除了a、b属性值
```

**@NonNull**

调用字段的setter方法时，如果传的参数为null，则会抛出空异常NullPointerException，生成setter方法时会对参数是否为空检查



**@NoArgsConstructor**

生成无参构造函数。但是类中有final字段没有初始化的时候，编译器会报错。加上参数，即@NoArgsConstructor(force = true)，然后就会为没有初始化的final字段设置默认值 0 / false / null,，此时，对于有@NotNull的字段就不会起作用.类中含有final修饰的成员变量，是无法使用@NoArgsConstructor注解的。

**@RequiredArgsConstructor**

所有带有@NonNull注解的或者带有final修饰的非静态I成员变量生成对应的构造方法。

**@AllArgsConstructor**

生成所有参数的构造函数

**@Cleanup**

这个注解用在变量前面，可以保证此变量代表的资源会被自动关闭，默认是调用资源的close()方法，如果该资源有其它关闭方法，可使用@Cleanup(“methodName”)来指定要调用的方法。

**@Data注解**

@Data = @Getter + @Setter + @ToString + @EqualsAndHashCode + @RequiredArgsConstructor 

```java
@Getter
@Setter
private int age;
```

如为final属性，则不会为该属性生成setter方法。`@Value`注解和`@Data`类似，区别在于它会把所有成员变量默认定义为private final修饰，并且不会生成set方法。

**@SneakyThrows**

加在方法上，表示将方法中的代码用try-catch语句包裹起来，捕获异常并在catch中用Lombok.sneakyThrow(e)把异常抛出，可以使用@SneakyThrows(Exception.class)的形式指定抛出哪种异常，

例子：

```java
@SneakyThrows(UnsupportedEncodingException.class)
    public String utf8ToString(byte[] bytes) {
        return new String(bytes, "UTF-8");
    }
```

相当于：

```java
 public String utf8ToString(byte[] bytes) {
        try{
            return new String(bytes, "UTF-8");
        }catch(UnsupportedEncodingException uee){
            throw Lombok.sneakyThrow(uee);
        }
    }
```



**@Synchronized**

这个注解用在方法上，效果和synchronized关键字相同。区别在于锁对象不同，对于类方法，synchronized关键字的锁对象是类的class对象；对于实例方法，synchronized关键字的锁对象是this对象，而@Synchronized得锁对象分别是私有静态final对象LOCK和私有final对象lock，也可以自己指定锁对象，

```
public class test {
    private final Object readLock = new Object();
 
    @Synchronized
    public static void hello() {
        System.out.println("world");
    }
 
    @Synchronized
    public int answerToLife() {
        return 42;
    }
 
    @Synchronized("readLock")
    public void foo() {
        System.out.println("bar");
    }
}
```

相当于：



```java
public class Synchronized {
   private static final Object $LOCK = new Object[0];
    //会自动创建锁对象
   private final Object $lock = new Object[0];
   private final Object readLock = new Object();
 
   public static void hello() {
       //static修饰的函数，用static final修饰的锁对象
     synchronized($LOCK) {
       System.out.println("world");
     }
   }
 
   public int answerToLife() {
       // //实例方法，用final修饰的锁对象
     synchronized($lock) {
       return 42;
     }
   }
 
   public void foo() {
     synchronized(readLock) {
       System.out.println("bar");
     }
   }
 }
```

**@Log**

用在类上，可以省去从日志工厂生成日志对象这一步，直接进行日志记录。

```java
@CommonsLog
//等价于
//private static final org.apache.commons.logging.Log log = org.apache.commons.logging.LogFactory.getLog(LogExample.class);
@JBossLog
//等价于
//private static final org.jboss.logging.Logger log = org.jboss.logging.Logger.getLogger(LogExample.class);
@Log
//等价于
private static final java.util.logging.Logger log = java.util.logging.Logger.getLogger(LogExample.class.getName());
@Log4j
//等价于
private static final org.apache.log4j.Logger log = org.apache.log4j.Logger.getLogger(LogExample.class);
@Log4j2
//等价于
private static final org.apache.logging.log4j.Logger log = org.apache.logging.log4j.LogManager.getLogger(LogExample.class);
@Slf4j
//等价于
private static final org.slf4j.Logger log = org.slf4j.LoggerFactory.getLogger(LogExample.class);
@XSlf4j
//等价于
private static final org.slf4j.ext.XLogger log = org.slf4j.ext.XLoggerFactory.getXLogger(LogExample.class);
//以上区别在于使用了不同的日志框架
```

java的类方法和实例方法：

类方法：就是static修饰的方法，即静态方法。

由于类方法是属于整个类的，所以类方法的方法体中不能有与类的对象有关的内容。
即类方法体有如下限制：
1.类方法中不能引用对象变量；
2.类方法中不能调用类的对象方法；
3.在类方法中不能调使用super，this关键字；
4.类方法不能被覆盖。

实例方法：类中没有static修饰的方法

当一个类创建了一个对象后，这个对象就可以调用该类的方法（对象方法）



缺点：

**侵入性太强：**Lombok 的使用要求开发者一定要在 IDE 中安装对应的插件，如果项目组中使用了 Lombok，那么所有开发人员都必须安装 IDE 插件，否则就没办法协同开发。侵入性太强，会给项目升级带来问题。

**降低代码可读性：**使用了Lombok在编译阶段才会生成的，在开发的过程中，其实很多代码其实是缺失的，就导致代码的可读性降低，而且也会给代码调试带来一定的问题。比如，想要知道某个类中的某个属性的 Getter 方法都被哪些类引用的话，就没那么简单了。

**破坏封装性：**使用 Lombok 会破坏封装性

**有风险**：