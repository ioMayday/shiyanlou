 C++内功修炼笔记
 =============
[toc]
# 1 常用语法及函数总结
## String
## Vector
## 关联容器
## 迭代器
## 小技巧

# 1 常用语法及函数总结


## String

**stoi()功能： 将字符串转化为int数值**

stoi（字符串，起始位置，n进制），将 n 进制的字符串转化为十进制<br>
stoi(str, m, n); //将字符串 str 从 m 位置开始到末尾的字符串，n进制转换为十进制,若不写n，则按默认ascill码转换<br>
需包含 #include <string>

**substr()功能：取string的连续子序列**

substr (起始位置, 字符个数);<br>
用法：<br>
string s = "abcdef";<br>
cout << s.substr(0,2); //输出ab<br>

**int转string的方法 数字转字符**

(1)利用stringstream：

使用stringstream的时候要注意加#include"sstream"。比如说我要把int类型的23转为string类型，那么我可以这样实现：
```
int a = 23;
stringstream ss;
ss << a;
string s1 = ss.str();
```
(2)利用sprintf int->char[]

(3)利用itoa int->char[]

(4)利用to_string


## Vector

**int pos = distance(len.begin( ),len_position)**

计算vector对应前后迭代器位置差，返回len_postion地址处在vector的第几个位置<br>
len[pos]  等效于 *len_position<br>


## Numeric.h 计算库

**accumulate(len.begin(),len_position,0)** 

计算vector的对应范围内的数值和，头两个形参指定要累加的元素范围，第三个形参则是累加的初值<br>

## 关联容器

**map:关键字和对应数值**

if(ss >= 'A' && ss <= 'Z') mA[ss]++; //ss为关键字，将ss关键字的数值加1，初始值默认为0<br>
Map为有序关联容器，默认按ascii码的顺序对字符或数字排序<br>
map<char, int> mA;    //初始化map类型的mA，关键字类型为char，数值类型为int<br>

## 迭代器

**使用迭代器的for循环，简洁代码 for(auto &c:s)与for(auto c:s)**

在c11标准下可以执行的特殊格式的for循环语句，区别在于引用类型可以改变原来的值
```
#include<iostream>
using namespace std;
int main()
{
    string s("hello world");
    for(auto c:s)
    c='t';
    cout<<s<<endl;//结果为hello world
    for(auto &c:s)
    c='t';
    cout<<s<<endl; //结果为ttttttttttt
    return 0;
}
```
参考链接：https://blog.csdn.net/iv__vi/article/details/79806683

## 小技巧

**//简洁的if语句加赋值**
MaxLen = MaxLen<2*cur?  2*cur : MaxLen;

**//C++中比较字符时用 ' ' 字符串时用 " "**
错误：s[i]=="(" || s[i]==")"
正确：s[i]=='(' || s[i]==')'

**//清空栈，栈的清空没有现成函数**
#include <stack>
stack<int> s;
while(!s.empty())  s.pop();


