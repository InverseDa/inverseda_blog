---
title: C. DS顺序表--合并操作
date: 2022-04-21
tags:
- SeqList 顺序表
categories:
- 深大数据结构OJ
---

### 题目描述
建立顺序表的结构体，属性包括：数组、实际长度、最大长度（设定为1000）

已知两个递增序列，把两个序列的数据合并到顺序表中，并使得顺序表的数据递增有序

### 输入
第1行先输入n表示有n个数据，接着输入n个数据，表示第1个序列，要求数据递增互不等

第2行先输入m表示有m个数据，接着输入m个数据，表示第2个序列，要求数据递增互不等
### 输出
顺序表内容包括顺序表的实际长度和数据，数据之间用空格隔开

第1行输出创建后的顺序表内容

### 输入样例1
```cpp
3 11 33 55
5 22 44 66 88 99
```

### 输出样例1
```cpp
8 11 22 33 44 55 66 88 99 
```
### 源代码
```cpp
#include <iostream>
#include <algorithm>

using namespace std;
#define ok 1
#define error -1

class SeqList {
    int *list, maxsize, size;
public:
    SeqList();

    SeqList(int *arr, int *brr, int n, int m);

    ~SeqList();

    int list_size();

    void list_display();
};

SeqList::SeqList() {
    maxsize = 1000;
    size = 0;
    list = new int[maxsize];
}

SeqList::SeqList(int *arr, int *brr, int n, int m) {
    size = m + n;
    list = new int[size];
    for (int i = 0; i < n; i++) {
        list[i] = arr[i];
    }
    for (int i = n, k = 0; k < m; i++, k++) {
        list[i] = brr[k];
    }
    sort(list, list + size);
}

SeqList::~SeqList() {
    delete[]list;
}

int SeqList::list_size() {
    return size;
}

void SeqList::list_display() {
    cout << size << ' ';
    for (int i = 0; i < size; i++)
        cout << list[i] << ' ';
    cout << endl;
}

int main() {
    int m, n;
    cin >> n;
    int *arr = new int[n];
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }
    cin >> m;
    int *brr = new int[m];
    for (int i = 0; i < m; i++) {
        cin >> brr[i];
    }
    SeqList list3(arr, brr, n, m);
    list3.list_display();

    return 0;
}
```

