---
title: B. DS堆栈--行编辑
date: 2022-04-21
tags:
- Stack 栈
categories:
- 深大数据结构OJ
---

### 题目描述
使用C++的STL堆栈对象，编写程序实现行编辑功能。行编辑功能是：当输入#字符，则执行退格操作；如果无字符可退就不操作，不会报错

本程序默认不会显示#字符，所以连续输入多个#表示连续执行多次退格操作

每输入一行字符打回车则表示字符串结束

注意：必须使用堆栈实现，而且结果必须是正序输出

### 输入

第一行输入一个整数t，表示有t行字符串要输入
第二行起输入一行字符串，共输入t行

### 输出

每行输出最终处理后的结果，如果一行输入的字符串经过处理后没有字符输出，则直接输出NULL

### 输入样例1
```cpp
4
chinaa#
sb#zb#u
##shen###zhen###
chi##a#####
```

### 输出样例1
```cpp
china
szu
sz
NULL
```
### 源代码
```cpp
#include <stack>
#include <iostream>
#include <vector>

using namespace std;

int main() {
    int t;
    cin >> t;
    while (t--) {
        stack<char> s;
        string str;
        cin >> str;
        for (char &i : str) {
            if (i != '#') s.push(i);
            else if (!s.empty()) {
                s.pop();
            }
        }
        int size = s.size();
        if (size) {
            vector<char> output;
            for (int i = 0; i < size; i++) {
                output.push_back(s.top());
                s.pop();
            }
            for (auto it = output.rbegin(); it != output.rend(); it++)
                cout << *it;
        } else cout << "NULL";
        cout << endl;
    }
}
```

