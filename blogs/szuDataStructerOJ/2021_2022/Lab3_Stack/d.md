---
title: D. DS堆栈--迷宫求解
date: 2022-04-21
tags:
- Stack 栈
categories:
- 深大数据结构OJ
---

### 题目描述
给出一个N*N的迷宫矩阵示意图，从起点[0,0]出发，寻找路径到达终点[N-1, N-1]

要求使用堆栈对象来实现，具体算法参考课本3.2.4节51页
### 输入
第一行输入t，表示有t个迷宫

第二行输入n，表示第一个迷宫有n行n列

第三行起，输入迷宫每一行的每个方格的状态，0表示可通过，1表示不可通过

输入n行

以此类推输入下一个迷宫
### 输出
逐个输出迷宫的路径

如果迷宫不存在路径，则输出no path并回车

如果迷宫存在路径，将路径中每个方格的x和y坐标输出，从起点到终点，每输出四个方格就换行，最终以单词END结尾，具体格式参考示范数据

输出的代码参考如下：
```cpp
//path是保存路径的堆栈，堆栈中每个元素都包含x坐标和y坐标，用属性xp和yp表示
//path1是一个临时堆栈，把path的数据倒序输出到path1，使得路径按正序输出
    if (!path.empty())//找到路径
    {
        //......若干代码，实现path的数据导入path1
        i=0;
        //以下是输出路径的代码
        while (!path1.empty())
        {
            cpos = path1.top();
            if ( (++i)%4 == 0 )
                cout<<'['<<cpos.xp<<','<<cpos.yp<<']'<<"--"<<endl;
            else
                cout<<'['<<cpos.xp<<','<<cpos.yp<<']'<<"--";
            path1.pop();
        }
        cout<<"END"<<endl;
    }
    else cout<<"no path"<<endl; //找不到路径输出no path
```
### 输入样例1
```cpp
2
8
0 0 0 1 1 1 1 1
1 0 0 0 1 0 0 1
1 0 0 0 1 0 0 0
1 1 0 0 0 0 0 1
0 0 1 1 0 1 1 0
0 0 0 0 0 0 1 1
1 1 1 1 1 0 0 1
0 0 0 0 1 0 0 0
7
0 0 0 1 1 1 1
1 0 0 1 0 0 1
1 0 0 1 0 0 0
1 1 0 0 0 0 1
0 0 1 1 0 1 0
1 0 0 0 0 1 0
0 0 0 0 1 1 0
```

### 输出样例1
```cpp
[0,0]--[0,1]--[0,2]--[1,2]--
[1,3]--[2,3]--[3,3]--[3,4]--
[4,4]--[5,4]--[5,5]--[6,5]--
[6,6]--[7,6]--[7,7]--END
no path
```
### 源代码
```cpp
#include <stack>
#include <vector>
#include <iostream>

using namespace std;

int main() {
    int t;
    cin >> t;
    while (t--) {
        int n;
        cin >> n;
        vector<vector<int>> matrix(n, vector<int>(n));  //迷宫图
        vector<vector<int>> hash(n, vector<int>(n));    //用哈希表存储走过的路径，走过记为1
        stack<pair<int, int>> path;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                cin >> matrix[i][j];
        int i = 0, j = 0;
        path.push({i, j});
        hash[i][j] = 1;
        do {
            if (i == n - 1 && j == n - 1) break;
            //前条件保证了i，j不越界的情况
            if (n > j + 1 && !matrix[i][j + 1] && !hash[i][j + 1]) { //右边有路且没走过
                //走到该路，并把脚下的路记为走过
                hash[i][j + 1] = 1;
                path.push({i, ++j});
            } else if (n > i + 1 && !matrix[i + 1][j] && !hash[i + 1][j]) {   //下边有路且没走过
                hash[i + 1][j] = 1;
                path.push({++i, j});
            } else if (j - 1 >= 0 && !matrix[i][j - 1] && !hash[i][j - 1]) {   //左边有路且没走过
                hash[i][j - 1] = 1;
                path.push({i, --j});
            } else if (i - 1 >= 0 && !matrix[i - 1][j] && !hash[i - 1][j]) {   //上边有路且没走过
                hash[i - 1][j] = 1;
                path.push({--i, j});
            } else {    //无路可走，或者有路了但都走过，只能往回走
                i = path.top().first;
                j = path.top().second;
                //判断是否走过
                bool youbian = n > j + 1 && !matrix[i][j + 1] && !hash[i][j + 1], xiabian =
                        n > i + 1 && !matrix[i + 1][j] && !hash[i + 1][j], zuobian =
                        j - 1 >= 0 && !matrix[i][j - 1] && !hash[i][j - 1], shangbian =
                        i - 1 >= 0 && !matrix[i - 1][j] && !hash[i - 1][j];
                if (!(youbian || xiabian || zuobian || shangbian)) path.pop();
            }
        } while (!path.empty());

        vector<pair<int, int>> finalpath;
        int size = path.size();
        if (size == 0) cout << "no path" << endl;
        else {
            int cnt = 0;    //换行标识符
            for (int i = 0; i < size; i++) {
                finalpath.push_back(path.top());
                path.pop();
            }
            for (auto it = finalpath.rbegin(); it != finalpath.rend(); it++) {
                cout << "[" << it->first << "," << it->second << "]--";
                if (++cnt % 4 == 0) cout << endl;
            }
            cout << "END" << endl;
        }

    }
}
```