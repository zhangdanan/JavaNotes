### List、Set和Map三者的区别

**List**：有序的对象

**Set**：不允许重复的集合，不会有多个元素引用相同的对象。

**Map**：使用键值对存储，key不能重复，但两个key可以引用相同的对象。

### 集合底层数据结构

Collection

List

- Arraylist：数组
- Vector：数组
- LinkedList：双向链表

Set

- HashSet（无序，唯一）：基于HashMap实现，底层采用HashMap来保存元素。
- LinkedHashSet：继承与HashSet，内部通过LinkedHashMap来实现的，
- TreeSet（有序，唯一）：红黑树（自平衡的排序二叉树）

Map

- HashMap：JDK1.8之前由数组+链表组成的，链表则是主要为了解决哈希冲突而存在的（“拉链法”解决冲突）。JDK1.8以后在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为8）（将链表转换成红黑树前会判断，如果当前数组的长度小于 64，那么会选择先进行数组扩容，而不是转换为红黑树）时，将链表转化为红黑树，以减少搜索时间。
- LinkedHashMap： LinkedHashMap 继承自 HashMap，所以它的底层仍然是基于拉链式散列结构即由数组和链表或红黑树组成。另外，LinkedHashMap 在上面结构的基础上，增加了一条双向链表，使得上面的结构可以保持键值对的插入顺序。同时通过对链表进行相应的操作，实现了访问顺序相关逻辑。
- Hashtable：数组+链表组成，数组是HashMap的主体，链表则是为了解决哈希冲突存在的。