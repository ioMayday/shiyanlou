=== C++内功修炼笔记

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

