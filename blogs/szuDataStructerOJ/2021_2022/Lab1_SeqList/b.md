---
title: B. DS顺序表--连续操作
date: 2022-04-21
tags:
- SeqList 顺序表
categories:
- 深大数据结构OJ
---

### 题目描述
建立顺序表的类，属性包括：数组、实际长度、最大长度（设定为1000）

该类具有以下成员函数：

构造函数：实现顺序表的初始化。

插入多个数据的multiinsert(int i, int n, int item[])函数，实现在第i个位置，连续插入来自数组item的n个数据，即从位置i开始插入多个数据。

删除多个数据的multidel(int i, int n)函数，实现从第i个位置开始，连续删除n个数据，即从位置i开始删除多个数据。

编写main函数测试该顺序表类。

### 输入

第1行先输入n表示有n个数据，即n是实际长度；接着输入n个数据

第2行先输入i表示插入开始的位置，再输入k表示有k个插入数据，接着输入k个数据

第3行先输入i表示删除开始的位置，再输入k表示要删除k个数据

### 输出

顺序表内容包括顺序表的实际长度和数据，数据之间用空格隔开

第1行输出创建后的顺序表内容

第2行输出执行连续插入后的顺序表内容

第3行输出执行连续删除后的顺序表内容


### 输入样例1
```cpp
6 11 22 33 44 55 66
2 3 99 88 77
4 5
```

### 输出样例1
```cpp
6 11 22 33 44 55 66 
9 11 99 88 77 22 33 44 55 66 
4 11 99 88 66 
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

    SeqList(int *item, int n);

    ~SeqList();

    int multiinsert(int i, int n, int item[]);

    int multidel(int i, int n);

    void list_display();
};

SeqList::SeqList() {
    maxsize = 1000;
    size = 0;
    list = new int[maxsize];
}

SeqList::SeqList(int *item, int n) {
    size = n;
    list = new int[n];
    list = item;
}

SeqList::~SeqList() {
    delete[]list;
}

int SeqList::multiinsert(int i, int n, int item[]) {
    int k = 0;
    for (int j = size; j >= i - 1; j--) {
        list[j + n] = list[j];
    }
    for (int j = i - 1; j < i + n - 1; j++) {
        list[j] = item[k++];
    }
    size += n;
    return ok;
}

int SeqList::multidel(int i, int n) {
    for (int j = i - 1; j <= size; j++) {
        list[j] = list[j + n];
    }
    size -= n;
    return ok;
}

void SeqList::list_display() {
    cout << size << ' ';
    for (int i = 0; i < size; i++)
        cout << list[i] << ' ';
    cout << endl;
}

int main() {
    int n, pos;
    cin >> n;
    int *element = new int[n];
    for (int i = 0; i < n; i++) {
        cin >> element[i];
    }
    SeqList sqlist(element, n);
    sqlist.list_display();
    cin >> pos >> n;
    int *item = new int[n];
    for (int i = 0; i < n; i++) {
        cin >> item[i];
    }
    sqlist.multiinsert(pos, n, item);
    sqlist.list_display();

    cin >> pos >> n;
    sqlist.multidel(pos, n);
    sqlist.list_display();


    return 0;
}
```_

