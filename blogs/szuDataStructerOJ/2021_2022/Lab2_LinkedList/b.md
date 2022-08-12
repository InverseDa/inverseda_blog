---
title: B. DS单链表--结点交换
date: 2022-04-21
tags:
- LinkList 链表
categories:
- 深大数据结构OJ
---

### 题目描述
用C++实现含头结点的单链表，然后实现单链表的两个结点交换位置。

注意不能简单交换两个结点包含数据，必须通过修改指针来实现两个结点的位置交换

交换函数定义可以参考：

swap（int  pa, int pb)  //pa和pb表示两个结点在单链表的位置序号

swap (ListNode * p, ListNode * q)  //p和q表示指向两个结点的指针

### 输入

第1行先输入n表示有n个数据，接着输入n个数据

第2行输入要交换的两个结点位置

第3行输入要交换的两个结点位置

### 输出

第一行输出单链表创建后的所有数据，数据之间用空格隔开

第二行输出执行第1次交换操作后的单链表数据，数据之间用空格隔开

第三行输出执行第2次交换操作后的单链表数据，数据之间用空格隔开

如果发现输入位置不合法，输出字符串error，不必输出单链表


### 输入样例1
```cpp
5 11 22 33 44 55
1 4
2 6
```

### 输出样例1
```cpp
11 22 33 44 55 
44 22 33 11 55 
error
```
### 源代码
```cpp
#include "iostream"

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

    ListNode *LL_index(int i); //返回第i个节点的指针，不存在则返回NULL
    int LL_merge(LinkList &La, LinkList &Lb, LinkList &Lc);

    int LL_get(int i);              //获取第i个节点
    int LL_insert(int i, int item); //在第i的位置插入新节点
    int LL_del(int i);              //删除第i个节点
    void LL_display();              //输出
};

LinkList::LinkList() {
    head = new ListNode;
    len = 0;
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

int LinkList::LL_merge(LinkList &La, LinkList &Lb, LinkList &Lc) {
    ListNode *p, *q, *r;
    p = La.head->next, q = Lb.head->next, Lc.head = r = La.head;
    while (p != nullptr && q != nullptr) {
        if (p->data <= q->data) {
            r->next = p;
            r = p;
            p = p->next;
        } else {
            r->next = q;
            r = q;
            q = q->next;
        }
    }
    r->next = p ? p : q;
    Lc.len = La.len + Lb.len;
    delete Lb.head;
    return ok;
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
    int n, m;
    cin >> n;
    LinkList la;
    for (int i = 1; i <= n; i++) {
        int val;
        cin >> val;
        la.LL_insert(i, val);
    }
    cin >> m;
    LinkList lb;
    for (int i = 1; i <= m; i++) {
        int val;
        cin >> val;
        lb.LL_insert(i, val);
    }
    LinkList lc;
    if (lc.LL_merge(la, lb, lc) == ok) {
        lc.LL_display();
    }
    return 0;
}
```

