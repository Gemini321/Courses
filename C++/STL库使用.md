# STL库使用

## string

```C++
#include <iostream>
#include <string>
using namespace std;

// 构造函数
string s1();
string s2("Hello");    // string(str)
string s3("Hello", 1, 3); // string(str/c_str, begin_index, str_len) -> s3 = "ell"
string s4("Hello", 3);  // string(c_str, str_len) -> s4 = "Hel" （C字符串为取前str_len个字母）
string s5(s2, 3);      // string(str, begin_index) -> s5 = "lo" （string类为以begin_index为下标取子串）
string s6(5, '1');     // string(number, char) -> s6 = "11111"
string s7(s2);         // string(str)

// string的信息
string s("Hello");
cout << s.length() << " = " << s.size() << endl;
cout << s.capacity() << endl; // 重新分配内存前，string对象能包含的最大字符数

// string的比较(字典序)
cout << s1.compare(s2) << " = " << s1 > s2 << endl;
cout << s1.compare(2, 3, s2) << endl; // 在s1下标为2处取长度为3的子串与s2比较
cout << s1.compare(2, 3, s2, 1, 2) << endl; // 在s1下标为2处取长度为3的子串与s2在下标为1处取长度为2的子串比较

// string的插入、拼接、删除和替换
s.push_back('a');
s.insert(s1.begin(), '1');
s.insert(0, "Hello");
s = s1 + s2;
s = s1.append(s2);
s.erase(s.begin() + 1, s.begin() + 3); // 删除操作可以使用string迭代器
s.erase(1, 3);
s.replace(6, 5, "girl"); // 在下标为6处选择长度为5的子串并替换成"girl"

// string大小写转换
s[2] = tolower(s[2]);
transform(s.begin(), s.end(), s.begin(), ::toupper);

// string的查找
s.find("Hello", begin_index = 0);
s.find_first_of("djaso"); // 找出s中第一个属于"djaso"的字符下标

// string的分割和截取
s.substr(begin_index, len);
```

## vector

```C++
#include <iostream>
#include <vector>
using namespace std;

// 初始化
vector<int> v;
vector<int> v(10); // 元素个数为10的vector
vector<int> v(10, 1); // 元素个数为10且初始值均为1的vector
vector<int> v(v1); // 拷贝构造函数
vector<int> v(v1.begin(), v1.end()); // 使用迭代器初始化
vector<int> v(b, b + 7); // 使用数组的指针对v进行初始化

// 赋值
v.assign(v1.begin(), v1.end()); // 使用迭代器赋值
v.assign(10, 1); // 类似于初始化

// 访问元素
v.front();
v.back();
v[i];

// 元素的增加
v.push_back(x);
v.insert(v.begin() + 1, x);
v.insert(v.begin() + 1, 3, x); // 在下标为1处插入3个x
v.insert(v.begin() + 1, b + 2, b + 4); // 利用数组b为v插入

// 元素的删除
v.pop_back();
v.erase(v.begin() + 3);
v.erase(v.begin(), v.begin() + 3); // 删除下标为[0, 3)的元素
v.clear();

// vector的信息
v.size();
v.capacity(); // 返回v在内存中总共可以容纳的元素个数
v.resize(new_size); // 对v扩容，多删少补
v.resize(new_size, new_element); // 扩容的新元素其值为new_element

// 其他
v.swap(v1); // v与v1整体交换
v == v1;
```

## map

除map<K, V>外，map中还定义了以下三种数据类型：

> map<K, V>::key_type：表示map容器中，索引的类型  
> map<K, V>::mapped_type : 表示map容器中，键所关联的值的类型  
> map<K, V>::value_type : 表示一个pair类型（即pair<K, V>），它的first元素具有const map<K, V>::key_type类型，而second元素则有map<K, V>::mapped_type类型，使用i.first和i.second来访问

```C++
#include <iostream>
#include <map>
#include <string>
#include <vector>
#include <utility>
using namespace std;

// 添加元素
map<int, string> m;
m[0] = string("Hello");
m.insert(map<int, string>::value_type(1, "world"));
m.insert(pair<int, string>(2, "Hey"));
m.insert(make_pair(3, string("Judy")));
pair<map<int, string>::iterator, bool> Insert_pair; // 使用Insert_pair获取是否插入成功
Insert_pair = m.insert(pair<int, string>(2, "Boy"));
if(!Insert_pair.second) cout << "Error insert new element" << endl;

// 查找元素
cout << m[4] << endl; // 未找到则输出为空
map<int, string>::iterator iter = m.find(1);
if(iter == m.end()) cout << "Do not find" << endl;
else cout << "Find!" << endl;

// 删除元素
map<int, string>::iterator iter = m.find(1); // 迭代器删除
m.erase(iter); // 若键值对不存在，则程序段错误
bool erase_success = m.erase(1); // 关键字删除，未找到则跳过且返回0，若成功删除则返回1
m.erase(m.begin() + 1, m.end()); // 迭代器范围删除
m.clear();

// map的信息
m.size();
m.empty();
m.swap(m1);
map<int, string>::iterator iter = m.upper_bound(m.begin(), m.end(), string("world")); // 返回第一个值大于"world"的位置
```

## stack

```C++
#include <iostream>
#include <stack>
#include <string>
using namespace std;

stack<string> s;
s.empty();
s.pop();
s.push(string("Hello"));
s.size();
s.top();
```

## queue

```C++
#include <iostream>
#include <queue>
#include <string>
using namespace std;

queue<string> words;
words.front(); // 返回第一个元素的引用
words.back();
words.push(string("Hello"));
words.pop();
words.size();
words.empty();
words.emplace(string("Hello")); // 插入新元素至队尾，同push
```

## priority_queue

```C++
#include <iostream>
#include <queue>
#include <vector>
using namespace std;

struct tmp1{
    int x;
    tmp1(int a): x(a) {}
    bool operator < (const tmp1 & t1) { // 方法1：重载<运算符
        return x < t1.x; // 大顶堆
    }
};

struct cmp{ // 方法2：重写仿函数
    bool operator () (const tmp1 & t1, const tmp1 & t2) {
        return t1.x < t2.x; // 大顶堆
    }
};

priority_queue<tmp1, vector<tmp1>, tmp2> pq;
pq.push(tmp1(123)); // 其余操作与queue相同
```

## list

```C++
#include <iostream>
#include <list>
#include <algorithm>
using namespace std;

// 初始化与赋值
list<int> l;
list<int>::iterator iter;
l.assign(2, 10); // 将l的元素变为两个10

// 插入与删除
l.push_front(1);
l.push_back(2);
l.insert(l.begin() + 1, 100); // 在第二个结点处插入100
l.insert(l.begin() + 1, 2, 100); // 在第二个结点处插入两个100
l.insert(l.begin() + 1, l1.begin(), l1.begin() + 3); // 插入其他链表
l.pop_front();
l.pop_back();
l.erase(l.begin() + 1);
l.erase(l.begin(), l.begin() + 3);

// 转置、合并
l.reverse();
l.merge(l1);

// list的信息
l.front();
l.back();
l.empty();
l.size();

```
