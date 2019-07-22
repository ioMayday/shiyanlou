# shiyanlou


```

#include <iostream>
#include <vector>
#include <string>

using namespace std;

int main() {
    std::cout << "Hello World!\n";
    string s;
    cin >> s;
    
    vector<string> operatorExp; 
    vector<int> Val; 
    int i=0,j=0;
    
    //分离数值与运算符
    while(s[i] != '=')
    {
        if (s[i]<='9' && s[i]>='0') ++i; //读取数值
        else if (s[i]=='+' || s[i]=='-') //读取运算符
        {
            operatorExp.push_back(s[i]);
            Val.push_back(stoi(s,j,i));
            j = ++i;//下一个必然是数值
        }   
    }
    //进行计算
    
    int len = operatorExp.size();
    i=0;
    int result=Val[0];
    while(i<len)
    {
        if (operatorExp[i] == '+')
        {
            result = result + Val[i+1];
        }
        else(operatorExp[i] == '-')
        {
            result = result - Val[i+1];
        }
    }
    
    cout << result << endl;
    
    
}

```
