---
title: C. DS单链表--合并
date: 2022-04-21
tags:
- LinkList 链表
categories:
- 深大数据结构OJ
---

### 题目描述
假定两个单链表是递增有序，定义并实现以下函数，完成两个单链表的合并，继续保持递增有序

int LL_merge(ListNode *La, ListNode *Lb)

### 输入
第1行先输入n表示有n个数据，接着输入n个数据

第2行先输入m表示有M个数据，接着输入m个数据
### 输出
输出合并后的单链表数据，数据之间用空格隔开

### 输入样例1
```cpp
3 11 33 55
4 22 44 66 88
```

### 输出样例1
```cpp
11 22 33 44 55 66 88 
```
### 源代码
```cpp
#include "bits/stdc++.h"

using namespace std;
#define ok 0
#define error -1

class ListNode {
public:
    int data;
    ListNode *next;

    ListNode() {
        next = nullptr;
    }
};

class LinkList {
public:
    ListNode *head;
    int len;

    LinkList();

    ~LinkList();

    ListNode *LL_index(int i); //返回第i个节点的指针，不存在则返回NULL

    int swap(int pa, int pb);  //交换两个节点
    int LL_get(int i);              //获取第i个节点
    int LL_insert(int i, int item); //在第i的位置插入新节点
    int LL_del(int i);              //删除第i个节点
    void LL_display();              //输出
};

LinkList::LinkList() {
    head = new ListNode;
    len = 0;
}

LinkList::~LinkList() {
    ListNode *p, *q;
    p = head;
    while (p != nullptr) {
        q = p;
        p = p->next;
        delete q;
    }
    len = 0;
    head = nullptr;
}

int LinkList::swap(int pa, int pb) {
    int real_pa = pa - 1, real_pb = pb - 1, cnta = 0, cntb = 0;
    if (real_pa >= len || real_pb >= len || real_pa < 0 || real_pb < 0) return error;
    ListNode *p, *q, *pp = head, *qp = head, *qn;
    p = q = head->next;
    while (p != nullptr) {
        if (cnta == real_pa - 1) pp = p;
        if (cnta++ != real_pa) {
            p = p->next;
        } else {
            break;
        }
    }
    while (q != nullptr) {
        if (cntb == real_pb - 1) qp = q;
        if (cntb++ != real_pb) {
            q = q->next;
        } else {
            break;
        }
    }
    qn = q->next;
    pp->next = q;
    q->next = p->next;
    qp->next = p;
    p->next = qn;
    return ok;
}

//返回第i个节点的指针，不存在则返回NULL
ListNode *LinkList::LL_index(int i) {
    int real_pos = i - 1, cnt = -1;
    if (real_pos >= len || real_pos < 0)
        return nullptr;
    ListNode *p = head;
    while (p != nullptr) {
        if (cnt++ != real_pos) {
            p = p->next;
        } else {
            return p;
        }
    }
    return nullptr;
}

int LinkList::LL_get(int i) {
    int cnt = 0, real_pos = i - 1;
    ListNode *p = head;
    if (real_pos >= len || real_pos < 0)
        return error;
    while (p != nullptr) {
        p = p->next;
        if (cnt++ == real_pos)
            return p->data;
    }
    return error;
}

int LinkList::LL_insert(int i, int item) {
    int real_pos = i - 1, cnt = 0;
    ListNode *p;
    p = head;
    if (real_pos > len || real_pos < 0)
        return error;
    while (p != nullptr) {
        if (cnt++ != real_pos) {
            p = p->next;
        } else {
            ListNode *q = new ListNode();
            q->next = p->next;
            p->next = q;
            q->data = item;
            len++;
            return ok;
        }
    }
    return error;
}

int LinkList::LL_del(int i) {
    int real_pos = i - 1, cnt = 0;
    if (real_pos > len || real_pos < 0)
        return error;
    ListNode *p = head;
    while (p != nullptr) {
        if (cnt++ != real_pos) {
            p = p->next;
        } else {
            ListNode *q = p->next, *r = p->next->next;
            delete q;
            p->next = r;
            len--;
            return ok;
        }
    }
    return error;
}

void LinkList::LL_display() {
    ListNode *p;
    p = head->next;
    while (p != nullptr) {
        //if (p != head) cout << ' ';
        cout << p->data << ' ';
        p = p->next;
    }
    cout << endl;
}

int main() {
    int n, pos1, pos2;
    LinkList list;
    cin >> n;
    for (int i = 1; i <= n; i++) {
        int val;
        cin >> val;
        list.LL_insert(i, val);
    }
    list.LL_display();

    cin >> pos1 >> pos2;
    if (list.swap(pos1, pos2) == ok) list.LL_display();
    else cout << "error" << endl;

    cin >> pos1 >> pos2;
    if (list.swap(pos1, pos2) == ok) list.LL_display();
    else cout << "error" << endl;
}
```

