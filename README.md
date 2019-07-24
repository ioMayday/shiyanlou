# shiyanlou


## C++ 常用语法及函数总结

*stoi() 将字符串转化为int数值，需包含 #include <string>*
stoi（字符串，起始位置，n进制），将 n 进制的字符串转化为十进制
stoi(str, m, n); //将字符串 str 从 m 位置开始到末尾的字符串，n进制转换为十进制,若不写n，则按默认ascill码转换

substr() string的子函数 **substr (起始位置, 字符个数);


## 华为机考题

**华为2019机考题目1，方法一 C++代码如下**
```
// 华为2019机考题目1
//https: //blog.csdn.net/lyxleft/article/details/88698136
//Autor: TOMD
//Date: 2019年7月24日 15:02:42
// 方法一：取出加减号和数值，再分开进行运算

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

**华为2019机考题目1，方法二 C++代码如下**
```

// 华为2019机考题目1
//https: //blog.csdn.net/lyxleft/article/details/88698136
//Autor: TOMD
//Date: 2019年7月24日 15:02:42
// 方法二：负号直接将负值赋给对应数值再累加

#include <iostream>
#include <vector>
#include <string> //包涵stoi()

using namespace std;

int main() {

    cout << "Hello World!"<< endl <<"The expression must end with <=> ! \n";
    string s,s_val;
    cin >> s;

    int len = s.length();
    int i=0,j=0,sum_val=0,temp_int=0;
    int flag_sgn=1;//默认为正，检测到负号后变为-1

    //检测表达式是否输入正确
    if (s[len-1] != '=')   {    //检测是否以等号结尾
            cout << "The input expression is wrong! Please input correctly again!" <<endl;
            return 0;
    }

    while(i<len)
    {
        if ((s[i]<='9' && s[i]>='0') || s[i]=='+' || s[i]=='-' || s[i] == '=') ++i; //检测是否为数值及加减符号
        else {
                cout << "The input expression is wrong! Please input correctly again!" <<endl;
                return 0;
        }
    }
    i=0;//使用完i后置零，以便下个循环用


    //提取数值并运算
    while(i<len)
    {
        if (s[i]<='9' && s[i]>='0') ++i; //读取数值
        else if (s[i]=='+' || s[i]=='-' || s[i] == '=') //读取运算符
        {

            s_val = s.substr(j,i-j); //string substr (起始位置, 字符个数);
            temp_int = flag_sgn*stoi(s_val); //用上一次的flag_sgn乘下一个读出来的数值，从第0位开始，将2进制的字符串转化为10进制数字,直接将 stoi(s,0,2)对其cout会报错
            temp_int = temp_int; //
            sum_val += temp_int; //累加计数到sum中

            if ( s[i] == '-')   flag_sgn = -1;
            else if( s[i] == '+') flag_sgn = 1;

            j = ++i;//移动到下一个数值起始位置，默认下一个必需是数值
        }

    }

    cout <<"The calculation is " << s << sum_val << endl;

    while (1)
    {
       //让控制窗一直显示
    }

    return sum_val;

}


```
