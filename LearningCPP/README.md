[toc]
 C++内功修炼笔记
 =============
# 1 常用语法及函数总结
## String
## Vector
## 关联容器
## 迭代器
## 小技巧


# 1 常用语法及函数总结

## 基础语法
**运算符号优先顺序表**
```
1级优先级 左结合
() 圆括号
[] 下标运算符
-> 指向结构体成员运算符
. 结构体成员运算符
2级优先级 右结合
! 逻辑非运算符
~ 按位取反运算符
++ 自增运算符
-- 自减运算符
- 负号运算符
(类型) 类型转换运算符
* 指针运算符
& 地址与运算符
sizeof 长度运算符
3级优先级 左结合
* 乘法运算符
/ 除法运算符
% 取余运算符
4级优先级 左结合
+ 加法运算符
- 减法运算符
5级优先级 左结合
<< 左移运算符
>> 右移运算符
6级优先级 左结合
<、<=、>、>= 关系运算符
7级优先级 左结合
== 等于运算符
!= 不等于运算符
8级优先级 左结合
& 按位与运算符
9级优先级 左结合
^ 按位异或运算符
10级优先级 左结合
| 按位或运算符
11级优先级 左结合
&& 逻辑与运算符
12级优先级 左结合
|| 逻辑或运算符
13级优先级 右结合
? : 条件运算符
14级优先级 右结合
= += -= *= /= %= &= ^= |= <<= >>= 全为赋值运算符
15级优先级 左结合
， 逗号运算符


优先级:自上到下由高到低
｜（）｛｝〔〕．（结构体成员运算符）－＞（指向结构体成员运算符）
｜单目运算符 ！（非）－－（自减）＋＋（自加）～（按位取反）
｜算术运算符+ - * % /
｜关系运算符< > >= <= ==
｜&&和||
｜赋值运算符 =
｜逗号运算符 （表达式1），（表达式2），（表达式3）．．．
还有就是左右运算顺序
a+b +为双目运算符, (a>b)?a:b 中? :为3目运算符． ！a 为单目运算符.
单目，三目运算符都为自右向左结合，双目运算符除赋值运算符都为自左向右结合
```

 
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

**erase函数的使用总结**
https://www.cnblogs.com/ylwn817/articles/1967689.html

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

**单个字符与0-9的数字相互转换**
```
//1）转数字
char ch = '5';
int a = ch - '0'; //利用ASCII码做差

//2) 转字符
int a = 5;
char ch = a + '0';
```

**string中 size()与length()**

说明：作用是相同的，都是返回字符串长度。

## Vector

**int pos = distance(len.begin( ),len_position)**

计算vector对应前后迭代器位置差，返回len_postion地址处在vector的第几个位置<br>
len[pos]  等效于 *len_position<br>


## Numeric.h 计算库

**accumulate(len.begin(),len_position,0)** 

计算vector的对应范围内的数值和，头两个形参指定要累加的元素范围，第三个形参则是累加的初值<br>



**C/C++语言的标准库里包含求绝对值的函数abs()，头文件声明**
```
C语言中，
求整数的绝对值abs()和labs()应该包含stdlib.h
求浮点数的绝对值fabs()应该包含math.h

在C++中，
只需要包括cmath即可。
#include <cmath> //要用到abs或者fabs
````

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

**CodeBlocks中cout时中文字符串乱码**
```
例如：cout << "售卖件数：" << n << " 总售价：" << m << endl;
显示时，“售卖件数：”显示乱码，之后从n开始的显示正常，总售价显示正常，但把总售价前面的空格去掉也是乱码。

调试发现，中文字符串输出时，内部字符串前面加个空格即可解决。 怀疑是软件本身编译器的问题。
cout << " 售卖件数：" << n << " 总售价：" << m << endl;
cout << " 欢迎您！";
以上例子均可正常显示。

```

**快速注释及恢复一段块代码**

```
使用以下注释方法：

注释块：
/* ********
正常的代码
// ***** */

取消注释： （仅需由 / 的有无来控制）
//* ********
正常的代码
// ***** */


```

**Bug调试问题及技巧总结**

```
【例1】
string s(n,'0'); 
for (int i=0; i < s.length();i++) s[i] += i+1; 
//s[i] += i+1; 与 s[i] = i+1;不同，因为s是存的字符不是数字，前者等效于 s[i] = '0' + i + 1;
改成：
for (auto i : s)  s[i] += i+1;
//虽然可以简化代码，但是由于i为迭代器，不是下标，运行s[i] += i+1,会导致s的所有值均为0，达不到目标

//for (auto i : s) 这种简化代码用在
vector<int> nums;
unordered_map<int,bool> used;
for (auto i : nums) used[i] = false; //初始化默认均未用过
        

【例2】函数内子循环中声明变量与外部变量声明重名时如何处理？
        auto tmp = rfirst;
        auto change = rfirst;
        while(tmp != pivot) {
            if (*pivot < *tmp) {
                change = tmp;  //auto change = tmp，如果是用这句的话，change被tmp赋值后只是while里的局部变量，到swap中交换时，change还是最开始初始化的rfirst。
                break;
            }
            tmp = next(tmp);
        }   
   swap(*pivot,*change); //两个值交换
   
【例3】   
auto change = find_if(rfirst, pivot, bind1st(less<int>(),*pivot)); 
        //在rfirs,pivot的区间内找，第一个比pivot大的元素，find_if返回的是迭代器的地址
               //bind1st(less<int>(),*pivot) 这行代码的意思是：将pivot 绑定为第一个参数，即 pivot < value，value为在rfirst,pivot区间要找的值
               //bind2nd(less<int>(),*pivot) 则表示找 value < pivot
               
【例4】二维数组表达
matrix[i,],matrix[n-1-i,j]     错
matrix[i][j],matrix[n-1-i][j]  对

【例5】string的操作
s为string,count为 int
s.push_back(count+'0'); //s.push_back(count);  +'0'很重要涉及到字符与数字的转换
while (k < len) { // s[k+1] != '\0' 是c的表达来判断是否到结束，如果是string就判是否到末尾下标就行

```

