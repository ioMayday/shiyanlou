
# 1 机考准备

## 华为2019年3月机考题

链接参考：
https://blog.csdn.net/lyxleft/article/details/88698136
https://blog.csdn.net/qq_28584889/article/details/88706373


**题目1：从输入字符串中读取数据，计算百内加减法**

**方法一 C++代码**
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

**题目2：从输入字符串中读取所有的蛇形字符串，先按长度排序，长度相同的按字典序，输出**

```
#include <iostream>
#include <vector>
#include <string>
#include <map>
#include <set>
#include <algorithm>
#include <numeric> //用到求和函数
using namespace std;

//测试：SxxsrR^AaSs
//理论输出：RrSs Aa Ss

int main()
{
    cout << "Please input a correct string!"<<endl;
	string s;
	cin >> s;

// 测试区
//   string s = "SxxsrR^AaSs"; //已测试通过
//   string s = "DAFHAGFAHFIUHRjkfhbdajfhkEHFUWEIHAJSDKHncnthasrkjhaejsavbdcnskdscnjkdfhgbvsdfdnfkhgj&*(&%^&*(bdvdhjBSDZVBDFBDVH"; //已测试通过
   cout << "The input string is " << s << endl;
   
	map<char, int> mA, ma;//mA存大写字母，ma存小写字母
	vector<int> len;
	int count_num=1; //默认最小子字符串长为1

	for (auto ss : s)
	{
		if(ss >= 'A' && ss <= 'Z') mA[ss]++; //ss为关键字
		if(ss >= 'a' && ss <= 'z') ma[ss]++;
	}
	for (auto it = mA.begin(); it != mA.end();)
	{//mA每个关键字对应键值取mA和ma中最小
		if(ma.count(it->first + 32) == 1) //ascii码中A为65，a为97，相差32
		{
			it++;
		}else mA.erase(it++);//如果ma中没有，则在mA中删除此关键字
	}
	/*for (auto x : mA)//遍历mA中的元素
		cout << x.first << "  " << x.second << endl;*/

	if(mA.empty()){cout << "Not Found" << endl; system("pause"); return 0;}//没有找到

	string tmp,tmp1;
	map<char, int>::iterator pre, cur;
	while (!mA.empty())
	{
		pre = mA.begin();
		cur = mA.begin();
		if(cur->second == 0)
		{
			mA.erase(cur++);
			continue;
		}
		tmp += cur->first, tmp += cur->first + 32;
		cur->second--;//对应键值减一
		pre = cur, cur++;


		while (cur != mA.end() && cur->second > 0 && cur->first == pre->first + 1) //找寻连续的串
		{//继续往下查找的条件是没有到达结尾，当前的迭代器指向的键值不为0，并且与上一个字母是相邻的
			tmp += cur->first, tmp += cur->first + 32;
			cur->second--;
			pre++, cur++,count_num++;
		}

		len.push_back(count_num);
        count_num = 1; //每次查询后count_num置为1

		//cout << tmp << endl;
		//tmp.clear();
	}


    vector<int> len_sorted(len);
    vector<int> len_tmp(len);
    stable_sort(len_sorted.begin(), len_sorted.end());

    //输出检测出的蛇形字符串
    cout <<"All Serpentine string are " <<  tmp << endl;

    //按长度排序输出
    int start_pos=0;
    for (int i=len.size()-1; i>=0; i--)
    {
           auto len_position = find( len.begin( ), len.end( ), len_sorted[i] ); //找到对应值的位置 len_position为len的迭代器
           int pos = distance(len.begin( ),len_position);
           len[pos] = 0; //找到输出一个字符串就消掉len中对应的字符串长度，置为0

           if (pos == 0) start_pos = 0; //若起点是0位，则无法累加前面的，直接赋值即可
           else { //若起点是非0位，则应累加前面到第a位以前的所有数值，得到原来字符串的起点位置
                for (int j=0;j<pos;j++) start_pos=2*len_tmp[j]+start_pos;
           }

           //int start_pos = 2*accumulate(len_tmp.begin(),len_position,0); //计算的区间为左闭右开 [len.begin(),len_position)
           //accumulate(len.begin(),len_position,0) 头两个形参指定要累加的元素范围，第三个形参则是累加的初值

           cout << tmp.substr(start_pos,2*len_sorted[i]) <<", The length of substring is " << 2*len_sorted[i] <<endl; //输出对应长度的子字符串
           start_pos=0; //运算完后，起点默认位置归零,进入下一个循环输出字符串

    }

	tmp.clear();
	system("pause");  //暂停系统，即无限循环
	return 0;
}

```



# 2 面试准备

