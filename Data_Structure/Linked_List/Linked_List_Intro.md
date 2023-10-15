# 单链表
## C语言里是如何构造出链表的
节点是链表的基本单位，由数据域和指针域构造出。数据域是用来存放元素的值，而指针域则用来存放指针（下一个节点的地址）<br>
代码如下：
```C
// C语言
typedef struct link {
  char elem; // 数据
  struct link* next; // 指针
} Link;

// Leetcode
struct ListNode {
  int val;
  struct ListNode* next;
};

// 创建一个 1 2 3 4 5 的链表
struct ListNode* initLink() {
  int i;
  struct ListNode* p = NULL;
  struct ListNode* temp = (struct ListNode*)malloc(sizeof(struct ListNode));
  temp->val = 1;
  temp->next = NULL;
  p = temp;
  for (i = 2; i < 6; i++) {
    struct ListNode* a = (struct ListNode*)malloc(sizeof(struct ListNode));
    a->val = i;
    a->next = NULL;
    temp->next = a;
    temp = temp->next;
  }
  return p;
}
```

## 插入元素
1. 在链表头节点插入元素<br><br>
在表头插入元素的时候，我们只需要把新元素的指针指向头节点就好了。但是还需要更新head，让head表示头节点
```C
newNode->next = head;
head = newNode
```

2. 在链表中间插入元素<br><br>
在链表中间插入元素的时候，需要先让新节点的指针指向当前节点的下一个节点。假如直接让当前节点的指针直接指向新元素，后面的链表将会消失。
```C
newNode->next = curNode->next
curNode->next = newNode
```

3. 在链表尾节点插入元素<br><br>
在表尾插入元素就很简单了，只需要让尾节点指向新元素就可以
```C
endNode->next = newNode
```

## 删除元素
1. 删除头节点<br><br>
更新head为当前head的下一个节点即可
```C
head = head->next
```
  
3. 删除中间的节点<br><br>
把要删除的节点的上一个节点指向下一个节点
```C
prevNode->next = prevNode->next->next
```
   
5. 删除尾节点<br><br>
让尾节点的上一个节点指向NULL
```C
prevNode->next = NULL
```
<br>

# 双向链表
## C语言里是如何构造出双向链表的
相较于单链表，双向链表可以得到上一个节点的值和指针。构造的时候只需要加一个priorNode指针即可。
代码如下：
```C
// C语言
typedef struct link {
  char elem; // 数据
  struct link* next; // 下一个节点的指针
  struct link* prior; // 上一个节点的指针
} Link;

// Leetcode
struct ListNode {
  int val;
  struct ListNode* next;
  struct ListNode* prior;
};

// 创建一个 1 2 3 4 5 的链表
struct ListNode* initLink() {
  int i;
  struct ListNode* p = NULL;
  struct ListNode* temp = (struct ListNode*)malloc(sizeof(struct ListNode));
  temp->val = 1;
  temp->next = NULL;
  temp->prior = NULL;
  p = temp;
  for (i = 2; i < 6; i++) {
    struct ListNode* a = (struct ListNode*)malloc(sizeof(struct ListNode));
    a->val = i;
    a->next = NULL;
    a->prior = temp;
    temp->next = a;
    temp = temp->next;
  }
  return p;
}
```

## 插入元素
1. 在双向链表头节点插入元素<br><br>
在表头插入元素的时候，我们只需要把新元素的next指针指向头节点，prior指针指向NULL，且更新head
```C
newNode->next = head;
newNode->prior = NULL;
head = newNode
```

2. 在双向链表中间插入元素<br><br>
在双向链表中间插入元素的时候，需要先让新节点的next指向当前节点的下一个节点，prior指向当前节点。
```C
newNode->next = curNode->next
newNode->prior = curNode
curNode->next->prior = newNode
curNode->next = newNode
```

3. 在双向链表尾节点插入元素<br><br>
在表尾插入元素需要让尾节点的prior指向新元素，
```C
endNode->next = newNode
newNode->prior = endNode
```

## 删除元素
1. 删除头节点<br><br>
更新head为当前head的下一个节点，并且让已更新的head的prior指向NULL
```C
head = head->next
head->prior = NULL
```
  
3. 删除中间的节点<br><br>
把要删除的节点的上一个节点的next指向下一个节点，下一个节点的prior指向要删除的节点的上一个节点
```C
prevNode->next = prevNode->next->next
nextNode->prior = nextNode->prior->prior
```
   
5. 删除尾节点<br><br>
让尾节点的上一个节点的next指向NULL
```C
prevNode->next = NULL
```
