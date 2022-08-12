---
title: A. DS堆栈--逆序输出（STL栈使用）
date: 2022-04-21
tags:
- Stack 栈
categories:
- 深大数据结构OJ
---

### 题目描述
C++中已经自带堆栈对象stack，无需编写堆栈操作的具体实现代码。

本题目主要帮助大家熟悉stack对象的使用，然后实现字符串的逆序输出

输入一个字符串，按字符按输入顺序压入堆栈，然后根据堆栈后进先出的特点，做逆序输出

### 输入
第一行输入t，表示有t个测试实例
第二起，每一行输入一个字符串，注意字符串不要包含空格

字符串的输入可以考虑一下代码：
```cpp
#include <string>
int main()
{
    string str;
    int len;

    cin>>str; //把输入的字符串保存在变量str中

    len = str.length()  //获取输入字符串的长度
}
```
### 输出
每行逆序输出每一个字符串
### 输入样例1
```cpp
2
abcdef
aabbcc
```

### 输出样例1
```cpp
fedcba
ccbbaa
```
### 源代码
```cpp
#include <stack>
#include <iostream>

using namespace std;

int main() {
    string str;
    int size, t;
    stack<char> cs;
    cin >> t;
    cin.get();
    while (t--) {
        getline(cin, str);
        for (char &i : str) {
            cs.push(i);
        }
        size = cs.size();
        for (int i = 0; i < size; i++) {
            cout << cs.top();
            cs.pop();
        }
        cout << endl;
    }
}
```

