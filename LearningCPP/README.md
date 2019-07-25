# C++内功修炼笔记

## 1 常用语法及函数总结

*stoi() 将字符串转化为int数值，需包含 #include <string>*
stoi（字符串，起始位置，n进制），将 n 进制的字符串转化为十进制
stoi(str, m, n); //将字符串 str 从 m 位置开始到末尾的字符串，n进制转换为十进制,若不写n，则按默认ascill码转换

substr() string的子函数 **substr (起始位置, 字符个数);
