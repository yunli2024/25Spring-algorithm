# STL

平时写的时候多看多用，忘记了随用随查，逐渐就会记得很清楚了~		——yunli

STL容器，用于存放数据（类似于数组）

**1.vector容器** 初步介绍

是一个动态的数组 vector<int> v1;

vector数组是**支持随机访问的！** 有迭代器

支持随机访问指的是能用[] 操作符结合index去访问数组中任意位置的元素，且时间复杂度为O(1)

迭代器 相当于这个数组的指针。 vector<int>::iterator it=v1.begin(); 相当于定义了一个it指针，指向数组v1的开头那个元素。

前面的那一串vector<int>::iterator是迭代器的类型！也可以用auto替代。

v1.begin() 是数组首元素的位置（头指针） v1.end()是数组最后一个元素的**下一个位置**（尾指针）

注意STL容器都是左闭右开的，也就是说不能取到尾指针。

for(vector<int>::iterator it=v1.begin();it!=v1.end();it++)

cout<<*it<<" ";  因为迭代器是一个指针在移动，所以这里用 * 进行解指针，输出数组中元素

*v1.begin()等价于v1[0] 都是第一个位置的元素

**一些常用函数**

```cpp
vector<int> v({1,2,3});
v.size();
v.empty();
v.begin() v.end();
v.front();//返回第一个元素，等价于v[0] *v.begin()
v.back()//返回最后一个元素！等价于v[v.size()-1]
**重要的：尾部插入和删除**
v.push_back(4) v.pop_back();
这两个操作都是O(1)的时间复杂度~

```

**2.queue** 也是STL容器中一个很重要的数据结构！

#include<queue> 包含queue和优先队列priority_queue 注意是不支持随机访问的！

写STL的时候，核心就是知道每一个常用操作，以及他们的时间复杂度就可以了，而不需要去关注底层的细节，因为它本身就已经封装好了。甚至可以后面用到的时候再多补一下，就记住了。

```cpp
queue<int> q; //普通队列
q.push(1);
q.push(3);
q.push(2);
q.front();//查看队首元素是1
q.back();//查看队尾元素是2
q.pop();//弹出队首元素（先进先出~）
q.size() q.empty();

priority_queue<int> pq; //优先队列，默认大根堆，也就是适合pop最大数据的
pq.push(1);
pq.push(3);
pq.push(2);
pq.top();//返回最大的元素3
pq.pop();//弹出最大的元素2

priority_queue<int,vector<int>,greater<int>> min_pq;//重新定义一下优先队列，为小根堆
//此时top和pop都是对队列中最小的元素进行的操作

```

**3.stack** 

stack遵循先进后出的原则，不支持随机访问！

注意queue和stack都不能随机访问，使用他们的场合一般是需要非常严格的LIFO和FIFO逻辑，因此牺牲了一定的灵活性。

```cpp
stack<int> stk;
stk.push(1);
stk.push(3);
stk.top();//查看栈顶元素为3
stk.pop();//弹出栈顶元素，LIFO
stk.top();//栈顶元素为1了
```

**4.deque** 双端队列~

双端队列是一个功能很全面的STL容器~(但是好像还是vector用的最多hh)

它可以在两端高效插入和删除元素（相比之下vector只有一端） 同时还可以**支持随机访问！**

```cpp
deque<int> dq;
dq.push_back(1);
dq.push_front(3);//两端都可以插入
dq.front();
dq.back();//队头队尾都可以访问
dq[0];//支持随机访问
dq.pop_front();
dq.pop_back();//两端都可以弹出
dq.begin() dq.end() //可以生成对应的迭代器~
```

**5.set**

set用于存储唯一的元素，相当于一个集合。同时集合的内部也是默认升序排序的，所以查找起来比较快，时间复杂度是logn

有双向迭代器，但是不可以随机访问~

```cpp
set<int> s;
s.insert(3);//不是使用push进行插入了~
s.insert(2);
s.insert(3);//重复会被忽略掉
auto it=s.find(3) //find会返回一个set的迭代器！如果没有找到则这个迭代器等于end
if(it!=s.end()) s.erase(it); 找到了就可以删除~此处是通过迭代器进行删除
s.erase(2)  //也可以直接通过值进行删除
auto l=s.lower_bound(1) //返回大于等于1的最小元素的迭代器！
auto u=s.upper_bound(1)//此处是大于1的最小元素的迭代器!注意不要看字面意思哦~
//所有想要查找的情况，都是在对STL容器的迭代器进行操作吖
```

**6.map** 映射的数据结构，是一个二元组的形式，基于键值对的映射

底层结构其实是RBTree

```cpp
map<string,int> hash;
hash.insert({"a",1});//注意insert & erase都是对一个pair进行的，需要{}完整~
cout<<hash["a"]<<endl; //这里通过hash[key]来访问key指向的value
//累了，感觉差不多够用…
```

