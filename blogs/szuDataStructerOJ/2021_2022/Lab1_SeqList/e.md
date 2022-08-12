---
title: E. 计算2支股票的M天运动平均价格
date: 2022-04-21
tags:
- SeqList 顺序表
categories:
- 深大数据结构OJ
---

### 题目描述
给定2支股票的开盘价和收盘价的N天历史数据，

要求按开盘和收盘，分别计算每支股票的每个日期对应的M天移动平均价格。

假定两个股票数据如下：

日期            开盘/收盘      第1支股票价格S1       第2支股票价格S2

2004/7/29 close 6 4

2004/7/25 close 2 6

2004/7/26 open 8 12

2004/7/30 open 2 4

2004/7/27 close 8 10

2004/7/28 open 4 2

按M=2天计算移动平均价格，按先开盘，后收盘价，输出如下：（若某日期之前，没有M-1条的记录（日期不用连续），则不用输出）

2004/7/28 open 6 7

2004/7/30 open 3 3

2004/7/27 close 5 8

2004/7/29 close 7 7

其中, 2004/7/28日的S1的值为(8+4)/2 = 6， 即将2004/7/28和（最近1条记录2004/7/26，最近2条记录，最近M-1条记录）的价格，求和并计算平均。
### 输入
第1行：N天记录   M天平均

第2行到N+1行：N天2支股票的开盘与收盘价格（注意日期是无序的）

6  2

2004/7/29 close 6 4

2004/7/25 close 2 6

2004/7/26 open 8 12

2004/7/30 open 2 4

2004/7/27 close 8 10

2004/7/28 open 4 2
### 输出
每个日期的最近M条记录（包括该日期的价格在内）的平均价格（若某日期之前没有M-1条的记录（日期不用连续），则不用输出）

2004/7/28 open 6 7

2004/7/30 open 3 3

2004/7/27 close 5 8

2004/7/29 close 7 7
### 输入样例1
```cpp
6  2
2004/7/29  	close      6	 4
2004/7/25  	close      2      6
2004/7/26  	open      8      12
2004/7/30  	open      2      4
2004/7/27  	close      8      10
2004/7/28  	open      4       2
```

### 输出样例1
```cpp
2004/7/28 open 6 7
2004/7/30 open 3 3
2004/7/27 close 5 8
2004/7/29 close 7 7
```
### 源代码
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>

using namespace std;

class gupiao {
public:
    string date, mode;
    int s1, s2;
};

bool cmp(const gupiao &a, const gupiao &b) {
    return a.date < b.date;
}

int main() {
    int n, m;
    cin >> n >> m;
    vector<gupiao> fileclose;
    vector<gupiao> fileopen;
    for (int i = 0; i < n; i++) {
        string date, mode;
        int s1, s2;
        cin >> date >> mode >> s1 >> s2;
        if (mode == "close") fileclose.push_back({date, mode, s1, s2});
        else fileopen.push_back({date, mode, s1, s2});
    }
    sort(fileopen.begin(), fileopen.end(), cmp);
    sort(fileclose.begin(), fileclose.end(), cmp);

    for (int i = 0; i < fileopen.size() - 1; i++) {
        int cnt = 0, sum1 = 0, sum2 = 0;
        for (int j = i + 1; j < fileopen.size(); j++) {
            sum1 += fileopen[i].s1 + fileopen[j].s1;
            sum2 += fileopen[i].s2 + fileopen[j].s2;
            if (++cnt == m - 1) {
                int arc1 = sum1 / m, arc2 = sum2 / m;
                cout << fileopen[j].date << ' ' << fileopen[j].mode << ' ' << arc1 << ' ' << arc2 << endl;
                break;
            }
        }
    }

    for (int i = 0; i < fileclose.size() - 1; i++) {
        int cnt = 0, sum1 = 0, sum2 = 0;
        for (int j = i + 1; j < fileclose.size(); j++) {
            sum1 += fileclose[i].s1 + fileclose[j].s1;
            sum2 += fileclose[i].s2 + fileclose[j].s2;
            if (++cnt == m - 1) {
                int arc1 = sum1 / m, arc2 = sum2 / m;
                cout << fileclose[j].date << ' ' << fileclose[j].mode << ' ' << arc1 << ' ' << arc2 << endl;
                break;
            }
        }
    }
}
```

