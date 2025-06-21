> [源码链接：java/util/HashMap.java](https://nowjava.com/readcode/jdk8/4726)

# HashMap与TreeMap


# HashMap与HashTable


# HashMap的Hash算法
参考：[深入理解 hashcode() 和 HashMap 中的hash 算法](https://blog.csdn.net/q5706503/article/details/85114159)
```java
static final int hash(Object key) {
    int h;
    return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
}
```
即：
- 如果key为null，则hash值为0。
- 如果key不为null，则先获取key的hashCode值，再进行无符号右移操作。对hashCode(int类型)无符号右移16位，即低16位被高16位替换，然后高16位置0。原先的和右移后的做异或，即，hashcode的高16位和与hashcode无符号右移16位的结果进行异或运算，就得到key的hash值。

对比一下 JDK1.7 的 HashMap 的 hash 方法源码:
```java
static int hash(int h) {
    h ^= (h >>> 20) ^ (h >>> 12);
    return h ^ (h >>> 7) ^ (h >>> 4);
}
```
相比于 JDK1.8 的 hash 方法 ，JDK 1.7 的 hash 方法的性能会稍差一点点，因为毕竟扰动了 4 次。


# HashMap扩容机制
为什么是2的幂次？

加载因子

# HashMap冲突解决
写函数，见`putVal`函数。
怎么判重，怎么写入








#HashMap