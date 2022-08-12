---
title: D. DS顺序表之循环移位
date: 2022-04-21
tags:
- SeqList 顺序表
categories:
- 深大数据结构OJ
---

### 题目描述
顺序表的移位是循环移位，例如顺序表：1，2，3，4，5，6。如果左移1位，即原来的头元素移动到末尾，其它元素向左移1位，变成2，3，4，5，6，1。同理，如果右移1位，即原来的尾元素移动到头，其它元素向右移1位，变成6，1，2，3，4，5。以下是移位的多个例子：

原数据：1，2，3，4，5，6

左移3位：4，5，6，1，2，3，与原数据对比

右移4位：3，4，5，6，1，2，与原数据对比

请编写程序实现顺序表的循环移位操作
### 输入
第1行输入n表示顺序表包含的·n个数据

第2行输入n个数据，数据是小于100的正整数

第3行输入移动方向和移动的位数，左移方向为0，右移方向为1

第4行输入移动方向和移动的位数，左移方向为0，右移方向为1

注意：移动操作是针对上一次移动后的结果进行的
### 输出
第一行输出创建后，顺序表内的所有数据，数据之间用空格隔开

第二行输出第一次移位操作后，顺序表内的所有数据，数据之间用空格隔开

第三行输出第二次移位操作后，顺序表内的所有数据，数据之间用空格隔开
### 输入样例1
```cpp
5
11 22 33 44 55
0 2
1 4
```

### 输出样例1
```cpp
11 22 33 44 55 
33 44 55 11 22 
44 55 11 22 33 
```
### 源代码
```cpp
#include <iostream>

using namespace std;
#define ok 1
#define error -1

class SeqList {
    int *list, maxsize, size;
public:
    SeqList();

    SeqList(int n, int *item);

    ~SeqList();

    int list_size();

    int list_move(int mode, int n);

    void list_display();
};

SeqList::SeqList() {
    maxsize = 1000;
    size = 0;
    list = new int[maxsize];
}

SeqList::SeqList(int n, int *item) {
    size = n;
    list = new int[n];
    list = item;
}

SeqList::~SeqList() {
    delete[]list;
}

int SeqList::list_size() {
    return size;
}

int SeqList::list_move(int mode, int n) {
    if (mode) {
        for (int i = 0; i < n; i++) {
            for (int j = size - 1; j >= 0; j--) {
                list[j + 1] = list[j];
            }
            list[0] = list[size];
        }
    } else {
        for (int i = 0; i < size - n; i++) {
            for (int j = size - 1; j >= 0; j--) {
                list[j + 1] = list[j];
            }
            list[0] = list[size];
        }
    }
}

void SeqList::list_display() {
    for (int i = 0; i < size; i++)
        cout << list[i] << ' ';
    cout << endl;
}

int main() {
    int n, item, mode;
    cin >> n;
    int *element = new int[n];
    for (int i = 0; i < n; i++) {
        cin >> element[i];
    }
    SeqList sqlist(n, element);
    sqlist.list_display();
    cin >> mode >> n;
    sqlist.list_move(mode, n);
    sqlist.list_display();
    cin >> mode >> n;
    sqlist.list_move(mode, n);
    sqlist.list_display();

    return 0;
}
```

