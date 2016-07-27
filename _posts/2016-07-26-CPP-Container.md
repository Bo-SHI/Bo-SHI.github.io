---
layout: post
title: "CPP Container"
date: 2016-07-26
---

# 容器  

- 标准库定义的容器分为 顺序容器 和 关联容器  
- 顺序容器 内的元素按其位置存储和访问  
- 关联容器 其元素按键排序  
- 容器类共享公共的接口  
  
> 将单一类型的元素聚集起来成为容器，然后按照位置来存储和访问这些元素，这就是顺序容器。  
> 顺序容器的排列次序与元素值无关，而是由元素添加到容器内的次序决定。  
> 标准库定义了三种顺序容器: vector list deque   
> 标准库的三种顺序容器的差别在于访问元素的方式以及添加删除元素相关操作的运行代价
> 标准库提供的三种适配器: stack queue priority_queue

## 顺序容器  
  
#### 顺序容器的初始化  

- 默认构造函数 C<T> c
- 将一个容器初始化为另一个容器的副本 C<T> c(c2) 创建容器c2的副本c，要求两个容器的类型和内部元素完全相同
- 初始化为一段元素的副本 C<T> c(b, e)  b和e是迭代器
- 分配和初始化指定数目的元素 C<T> c(n, t)  C<T> c(n)  NOTE: 只适用于顺序容器

> 当不使用默认构造函数，而是使用其他的构造函数初始化容器时，必须指出该容器有多少个元素，并提供这些元素的初值

#### 容器内元素的约定类型  

> 容器内的元素必须满足两个约定:  
>  > - 元素类型必须支持赋值运算符
>  > - 元素类型的对象必须可以被复制


- 支持赋值和复制功能是容器元素的最基本要求。  
- 某些容器操作对容器内的元素类型有特殊要求。
- 容器内的容器 书写的时候 注意用空格隔开两个相邻的 > 符号。  


## 迭代器和迭代器的范围  

> - 所有迭代器都支持的运算 : 解引用 自增自减 关系操作符 == 和 !=     
> - vector 和 deque 额外支持的运算 ： 迭代器算术运算 + - += -= 关系操作符 >= <= > <

> 只有vector和deque两种容器提供对其元素快速随机的访问。  

> - 迭代器范围 为左闭合区间  

> - 对形成迭代器范围的迭代器的要求:
> > - 指向同一个容器中的元素或者超出末端的下一个位置
> > - 如果这两个迭代器不相等，则对first迭代器反复坐自增运算必须能够达到last。换句话说，last决不能位于first之前  


## 顺序容器的操作  

  
#### 容器定义的类型别名

- size_type 无符号整型 
- iterator 迭代器类型 
- const_iterator 只读迭代器类型 
- reverse_iterator 逆序迭代器
- const_reverse_iterator 只读的逆序迭代器
- difference_type 迭代器差值的有符号整型，可为负值 
- value_type 元素类型 
- reference 元素的左值类型 等效于 value_type&  
- const_reference 元素的常量左值类型 等效于 const value_type& 

  
#### 在顺序容器中添加元素

- c.push_pack(t) 在容器c的尾部添加 所有的顺序容器都支持 
- c.push_front(t) 在容器c的前端添加 list deque 两种顺序容器支持 
- c.insert(p, t) 在迭代器p所指的元素之前添加 返回值新添加元素的迭代器 
- c.isnert(p, n, t) 
- c.insert(p, begin, end) 
  
  
> 在容器元素内添加的元素都是副本  
> 任何insert和push操作都有可能使迭代器失效 
> 避免存储end返回的迭代器 
  
  
#### 容器大小的操作 

- c.size()
- c.max_size()
- c.empty()
- c.resize(n)
- c.resize(n, t)  
  
> resize 操作可能会使迭代器失效  
  
  
#### 访问元素  
  
- c.back()
- c.front()
- c[n]  只适用于 vector deque
- c.at(n) 只适用于 vector deque  

#### 删除元素 

- c.erase(p) 删除迭代器p指向的元素 返回值为被删除元素后面元素的迭代器
- c.erase(b, e) 删除迭代器b和e所指范围的元素 返回值为被删除元素段后面的元素，若e指向超出末端的下一个位置，则返回值也为超出末端位置的迭代器
- c.clear() 删除所有的
- c.pop_back() 
- c.pop_front() 只适用于 list deque

  
#### 赋值和swap

- c1 = c2 赋值操作符首先删除左操作数容器内的所有元素，然后将右操作数容器的所有元素插入到左边容器。c1和c2的类型必须完全相同
- c.assign(b,e) 
- c.assign(n,t)
- c1.swap(c2) c1和c2类型必须完全相同 比赋值操作快  
  
> 赋值和assign操作会使左操作数的容器的所有迭代器失效。swap操作不会使迭代器失效。
> swap操作不会删除或插入任何元素，而且在常量时间内完成操作。 


#### vector容器的自增长  

> 为了使vector容器实现快速的内存分配，其实际分配的容量要比当前所需的空间多一些。  

- capacity 容器的容量大小
- reserve 分配容量的操作


#### 容器的选用

- vector容器 支持快速随机访问 但是插入和删除的开销较大
- list容器 表示不连续的存储区域 支持在任何位置可以快速插入删除 但不支持快速随机访问
- deque 
	- 与vector一样 在容器中间插入删除元素效率较低
	- 不同于vector deque提供在首部高效的插入删除 就像在尾部一样
	- 与vector一样 支持快速的随机访问
	- 在deque首部或尾部插入元素不会使任何迭代器失效，但在首部或尾部删除元素则只会使指向被删除元素的迭代器失效。在其他任何部位的插入删除操作会使所有迭代器失效。



## 关联容器

> 关联容器 ： map set multimap multiset  
> 关联容器通过支持键来高效的查找和读取元素


#### pair类型

- pair类型是标准库定义的一种类型
- pair.first pair.second 都是公有数据成员

#### 关联容器与顺序容器的一些操作异同

- 关联容器的构造 支持 默认构造 复制构造 迭代器构造 不支持顺序容器的通过大小来改造
- 关联容器 支持 begin end rbegin rend
- 关联容器 支持 类型别名 size_type (const_)iterator (const)_reverse_iterator difference_type value_type (const_)reference 
- 关联容器 支持 赋值操作和swap操作 但是不支持 assign 操作
- 关联容器 支持 erase clear 操作 但是返回值为void 顺序容器的返回值为被删除元素的下一个元素的迭代器
- 关联容器 支持 size max_size empty 但是不支持 resize
- 关联容器 不支持 front push_front pop_front back push_back push_front

#### map类型

> map 键类型的约束 所用的比较函数必须在键类型上定义 严格弱排序  
> 严格弱排序 如果一个键和自己比较，会导致false结果  

- map<K,V>::key_type 在map中，用作索引的键的类型
- map<K,V>::mapped_type 在map中，键所关联的值的类型
- map<K,V>::value_type 一个pair类型， first元素具有const map<K,V>::key_type类型， second元素具有map<K,V>::mapped_type类型

> map 下标操作符 map[map::key_type] = map::mapped_type  
	- 如果map中存在该键，则返回该键所关联的值
	- 如果map中不存在该键，map容器才为该键创建一个新的元素，并将它插入到map中。所关联的值先采用值初始化，然后再赋值。

> map insert操作符 map.insert(map::value_type) 
	- 如果map中存在该键，不做任何操作
	- 如果mao中不存在该键，则插入
	- 返回值为pair类型 pair<map::iterator, bool> bool为true则表明成功，否则失败(map中已经存在)  
  
> map count 查询key_type出现的次数 返回值为0或者1
> map find 查找map中key_type 返回值为迭代器  

> map erase
	- m.erase(k) 删除键为k的元素 返回值为删除的个数
	- m.erase(p) 删除迭代器指向的元素 返回值为void
	- m.erase(b, e) 删除迭代器范围内指向的元素 b,e必须为有效的 若b==e 则范围为空 返回值为void