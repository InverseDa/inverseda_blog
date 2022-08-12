---
title: E. DS线性表—多项式相加
date: 2022-04-21
tags:
- LinkList 链表
categories:
- 深大数据结构OJ
---

### 题目描述
对于一元多项式$p(x)=p_0+p_1x+p_2x^2+...+p_nx^n$，每个项都有系数和指数两部分，例如$p_2x^2$的系数为$p_2$,指数为$2$。

编程实现两个多项式的相加。

例如5+x+2x2+3x3，-5-x+6x2+4x4，两者相加结果：8x2+3x3+4x4

其中系数5和-5都是x的0次方的系数，相加后为0，所以不显示。x的1次方同理不显示。

要求用单链表实现。
### 输入
第1行：输入t表示有t组测试数据

第2行：输入n表示有第1组的第1个多项式包含n个项

第3行：输入第一项的系数和指数，以此类推输入n行

接着输入m表示第1组的第2个多项式包含m项

同理输入第2个多项式的m个项的系数和指数

参考上面输入第2组数据，以此类推输入t组

假设所有数据都是整数
### 输出
对于每1组数据，先用两行输出两个原来的多项式，再用一行输出运算结果，不必考虑结果全为0的情况

输出格式参考样本数据，格式要求包括：

1.如果指数或系数是负数，用小括号括起来。

2.如果系数为0，则该项不用输出。

3.如果指数不为0，则用符号^表示，例如x的3次方，表示为x^3。

4.多项式的每个项之间用符号+连接，每个+两边加1个空格隔开。
### 输入样例1
```cpp
2
4
5 0
1 1
2 2
3 3
4
-5 0
-1 1
6 2
4 4
3
-3 0
-5 1
2 2
4
9 -1
2 0
3 1
-2 2
```

### 输出样例1
```cpp
5 + 1x^1 + 2x^2 + 3x^3
(-5) + (-1)x^1 + 6x^2 + 4x^4
8x^2 + 3x^3 + 4x^4
(-3) + (-5)x^1 + 2x^2
9x^(-1) + 2 + 3x^1 + (-2)x^2
9x^(-1) + (-1) + (-2)x^1
```
### 源代码
```cpp
#include <iostream>
#include <string>
#include <cmath>

using namespace std;
#define ok 0
#define error -1
#define nullptr NULL

class ListNode {
public:
    int val;
    int exp;
    ListNode* next;

    ListNode() {
        next = nullptr;
    }
};

class LinkList {
public:
    ListNode* head;
    int len;

    LinkList();

    ~LinkList();

    int LL_insert(int i, int val, int exp); //在第i的位置插入新节点
    int LL_del(int i);              //删除第i个节点
    void LL_add(LinkList &La) const;
    void LL_display() const;              //输出
};

LinkList::LinkList() {
    head = new ListNode;
    len = 0;
}

LinkList::~LinkList() {
    ListNode* p, * q;
    p = head;
    while (p != nullptr) {
        q = p;
        p = p->next;
        delete q;
    }
    len = 0;
    head = nullptr;
}

int LinkList::LL_insert(int i, int val, int exp) {
    int real_pos = i - 1, cnt = 0;
    ListNode* p;
    p = head;
    if (real_pos > len || real_pos < 0)
        return error;
    while (p != nullptr) {
        if (cnt++ != real_pos) {
            p = p->next;
        }
        else {
            ListNode* q = new ListNode();
            q->next = p->next;
            p->next = q;
            q->val = val;
            q->exp = exp;
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
    ListNode* p = head;
    while (p != nullptr) {
        if (cnt++ != real_pos) {
            p = p->next;
        }
        else {
            ListNode* q = p->next, * r = p->next->next;
            delete q;
            p->next = r;
            len--;
            return ok;
        }
    }
    return error;
}

void LinkList::LL_add(LinkList &Lb) const {
    ListNode* p, * q;
    p = head->next;
    q = Lb.head->next;
    LinkList afterAddedList;
    ListNode* r = afterAddedList.head;
    while (p && q) {
        if (p->exp < q->exp) {
            r->next = new ListNode;
            r = r->next;
            r->exp = p->exp;
            r->val = p->val;
            p = p->next;
            afterAddedList.len++;
        }
        else if (p->exp > q->exp) {
            r->next = new ListNode;
            r = r->next;
            r->exp = q->exp;
            r->val = q->val;
            q = q->next;
            afterAddedList.len++;
        }
        else {
            if (p->val + q->val == 0) {
                p = p->next;
                q = q->next;
                continue;
            }
            r->next = new ListNode;
            r = r->next;
            r->exp = q->exp;
            r->val = p->val + q->val;
            p = p->next;
            q = q->next;
            afterAddedList.len++;
        }
    }
    while (p) {
        r->next = new ListNode;
        r = r->next;
        r->exp = p->exp;
        r->val = p->val;
        p = p->next;
        afterAddedList.len++;
    }
    while (q) {
        r->next = new ListNode;
        r = r->next;
        r->exp = q->exp;
        r->val = q->val;
        q = q->next;
        afterAddedList.len++;
    }
    r->next = nullptr;
    afterAddedList.LL_display();
}

void LinkList::LL_display() const {
    ListNode* p = head->next;
    for (int i = 0; i < len; i++) {
        if (p->val == 0) {
            p = p->next;
            continue;
        }
        printf("%s%s%d%s", p->val < 0 ? "(" : "", p->val < 0 ? "-" : "", abs(p->val), p->val < 0 ? ")" : "");//如果是负数，则输出（）
        printf("%s%s", p->exp == 0 ? "" : "x", p->exp != 0 ? "^" : "");
        if (p->exp != 0) printf("%s%s%d%s", p->exp < 0 ? "(" : "", p->exp < 0 ? "-" : "", abs(p->exp), p->exp < 0 ? ")" : "");

        if (i != len - 1) printf(" + ");
        p = p->next;
    }
    cout << endl;
}

int main() {
    int n;
    cin >> n;
    while (n--) {
        int a, b;
        cin >> a;
        LinkList La, Lb;
        for (int i = 1; i <= a; i++) {
            int val, exp;
            cin >> val >> exp;
            La.LL_insert(i, val, exp);
        }
        La.LL_display();
        cin >> b;
        for (int i = 1; i <= b; i++) {
            int val, exp;
            cin >> val >> exp;
            Lb.LL_insert(i, val, exp);
        }
        Lb.LL_display();
        La.LL_add(Lb);
    }
    return 0;
}
```

