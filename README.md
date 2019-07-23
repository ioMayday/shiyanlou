# shiyanlou


# C++ 常用语法及函数总结

*stoi() 将字符串转化为int数值，需包含 #include <string>*
stoi（字符串，起始位置，n进制），将 n 进制的字符串转化为十进制
stoi(str, m, n); //将字符串 str 从 m 位置开始到末尾的字符串，n进制转换为十进制,若不写n，则按默认ascill码转换

substr() string的子函数 **substr (起始位置, 字符个数);


# 华为机考题

**华为2019机考题目1，C++代码如下
```
// 华为2019机考题目1
//https: //blog.csdn.net/lyxleft/article/details/88698136
//Autor: TOMD

#include <iostream>
#include <vector>
#include <string> //包涵stoi()

using namespace std;

int main() {
    cout << "Hello World!\n";
    string s,s_val;
    cin >> s;

    vector<char> operatorExp;
    vector<int> Val;

    int len = s.length();
    int i=0,j=0;


    //分离数值与运算符
    while(i<len)
    {
        if (s[i]<='9' && s[i]>='0') ++i; //读取数值
        else if (s[i]=='+' || s[i]=='-' || s[i] == '=') //读取运算符
        {
            char temp_char = s[i];
            if ( temp_char != '=')   operatorExp.push_back(temp_char);

            s_val = s.substr(j,i-j); //string substr (起始位置, 字符个数);
            int temp_int = stoi(s_val); ////从第0位开始，将2进制的字符串转化为10进制数字,直接将 stoi(s,0,2)对其cout会报错
            Val.push_back(temp_int);
            j = ++i;//下一个必然是数值
        }
    }

    //进行计算
    len = operatorExp.size();
    i=0;
    int result=Val[0];

    while(i<len)
    {
        if (operatorExp[i] == '+')
        {
            result = result + Val[i+1];
        }
        else if (operatorExp[i] == '-')
        {
            result = result - Val[i+1];
        }
        ++i;
    }

    cout <<"The calculation is " << s << result << endl;

    while (1)
    {
       //让控制窗一直显示
    }

    return result;

}

```
