---
layout:     post
title:      "关于JAVA一些Collection的简单总结归纳"
date:       2017-06-01 11:39:00
author:     "CreeperSan"
header-img: "img/post/170507about/header.jpg"
tags:
    - JAVA
    - Collection
---

## 关于JAVA一些Collection的简单总结归纳

---
### List
1. ArrayList
    ArrayList擅长于随机访问元素，但是在List的中间插入和移除元素会比较慢。
2. LinkedList
    LinkedList在随机访问方面相对比较慢，但是在List中间插入和删除元素比ArrayList要快
3. 常用方法
    + `Collections.sort();`    //排序
    + `.contains()`    //判断某个对象是否在列表中
    + `.containAll()`//判断一组对象是否在List中（顺序不重要）
    + `.indexOf()`    //判断对象在List中的位置（下标）
    + `.subList()`  //从列表中创建一段列表
    + `.retainAll()`   //保留2个List中重复的部分，也就是2个List的交集，依赖于`equal()`方法
    + `.removeAll()` // 见名知意，也是依赖于`equal()`方法
    + `.set()`  //用于在指定索引位置处替换该位置的整个元素
    + `.isEmpty()`  //见名知意
    + `.clear()`    //见名知意

---

### LinkedList
+ LinkedList是双向列表，列表中的每一个节点都包含了对前一个和后一个元素的引用。使用链表可以实现类似栈和队列的操作。
+ `getFirst()`获取链表的第一个元素
+ `getLast()`获取链表的最后一个元素
+ `add()`添加元素，如果不指定位置，元素就会被增加到链表的最后
+ `addFirst()`添加元素到链表开始的地方,`addLast()`添加元素到链表的最后,其实`addFirst()`与不带索引的`add()`的效果是一样的
+ `removeFirst()`删除并返回链表的最开头的元素，`removeLast()`删除并返回链表的最后一个元素。如果没有则会报`NoSuchElementException`异常
+ `poll()`与`removeFirst()`、`remove()`方法类似，只不过没有的时候会返回空而不是抛异常
+ `push()`与`addFirst()`类似
+ `peek()`与`getFirst()`方法类似，只不过没有的时候会返回空而不是抛异常
+ `clear()`见名知意
+ `element()`返回但不移除头部的元素
+ `indexOf()`,`lastIndexOf()`见名知意
+ `offer()`把指定元素加到队列尾部

---

### 迭代器Iterator（也是一种设计模式，可以用于多种(List,Map,Set这些的集合类型)）

> 需要明确的一点是，迭代器指向的位置是元素之前的位置 ![](http://img.blog.csdn.net/20141127192847281?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbG9uZ3NoZW5nZ3Vvamk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

+ JAVA中的Iterator只能单向移动，这个Iteator只能用来做这些事情
    1. 使用方法`Iterator()`要求容器返回一个Iterator。这个Iteartor将准备返回序列的第一个元素。
    2. 使用`next()`方法来获得序列中的下一个元素（把元素堆到出口）
    3. 使用`hasNext()`方法来判断是否还有下一个元素
    4. 使用`remove()`方法来将迭代器的出口元素（新近返回的元素(由`next()`产生的最后一个元素)）删除
~~嗯，跟队列有点像啊~~
    
---

### ListIterator(仅能用于List的集合类型)
+ ListIterator是一个更加强大的Iterator的子类型，他只能用于各种List类的访问。尽管Iterator只能向前移动，但是ListIterator可以双向移动(`previous()`、 `next()`)。他还可以产生相对于迭代器在列表中指向的当前位置的前一个和后一个元素的索引，并且可以使用`set()`方法替换他访问过的最后一个元素。我们可以通过`listIterator()`方法创建一个指向List最开始出的ListIterator，也可以通过`listIterator(n)`方法来创建一个指向列表索引为n的ListIterator
+ ListIterator还能插入元素，通过`add()`能插入元素到迭代器当前位置之前(Iterator不可以)
+ `nextIndex()`返回迭代器所在位置后一元素的索引
+ `set()`返回迭代器`next()`或`previous()`的元素并迭代器中的这个元素修改成参数里的元素(Iterator只能删除，不能修改)


---

## Stack(栈)
> `栈`通常是指先进后出的容器。最后压入栈中的元素，最先被弹出栈。经常用于类比栈的事物是装有弹簧的储存器中的自动残托盘（？），最后装入的托盘总是最先被拿出来。

---

## Set

+ Set不保存重复的元素。Set具有与Collection一样的接口，因此没有额外的功能。Set是基于对象的值来确定归属性的。其中HashSet专门对快速查找做了优化。
+ Set的输出顺序没有规律可循，这是处于速度原因考虑的。
+ HashSet使用了散列，HashSet所维护的顺序与TreeSet或LinkedHashSet都不一样，因为他们的视线具有不同的元素存储方式。TreeSet将元素存储在红-黑树数据结构中,而HashSet使用的是散列函数。LinkedHashSet因为查询速度的原因也是使用了散列，但是它用链表来维护元素的插入顺序。
+ 实际上Set就是Collection,只是行为不同
+ 如果我们想制定排序顺序，那么我们可以向TreeSet的构造器中传入比较器，比如`String.CASE_INSENTIVE_ORDER`就是按照字母顺序排序。

---

### Map
+ HashMap是无序的，他根据HashCode的值存储数据，根据键可以获得值，具有很快的，访问速度。如果要实现同步，可以使用Collections.synchronizedMap或CurrentHashMap(?)
+ LinkedHashMap是HashMap的一个子类，键保存了插入的顺序，因此使用Iterator遍历是，得到的也是插入顺序的纪录。
+ TreeMap默认按键的升序排列，可以根据比较器来修改排序
+ *HashTable线程安全，键不能为null，但效率较低

---

## Queue队列
> 队列是一个先进先出的容器，即从容器的一端放入事物，从另一端取出。而且，其放入顺序与取出顺序是相同的

+ LinkedList提供了方法以及支持队列的行为，并且他实现了Queue接口。LInkedList可以向上转型为Queue
+ 常用方法
	+ `offer()`将一个元素插入到队尾，成功返回ture，失败返回false
	+ `peek()`返回队头但不移除，为空则返回null
	+ `element()`返回队头但不移除，为空则抛`NoSuchElement`异常
	+ `pull()`返回队头并移除，为空则返回null
	+ `remove()`返回队头并移除，为空则抛`NoSuchElement`异常

---

### 其他
+ `indexOf()` `remove()` `contains()` 都会用`equal()`来判断，那么当2个String是完全一样的时候，`equal()`会返回true！
+ `.toArray()` 返回一个当前对象集合的数组
