## 206. Reverse Linked List
##### 2018-03-30 16:22:31
##### 链表反转
***
## 1.题目
将一个链表反转，返回反转后的头，有递归与迭代两种写法。
## 2.分析
个人认为链表已经稍微掌握些了，但是看到这个题目之后没有什么直接的想法，更不敢说递归。  
看了别人的代码，解释下原理：  
#### 📌迭代：
1. 首先排除掉输入链表为空的情况。
2. 当输入不为空时，新建一个节点指针p，值为head->next,接着将head指向的元素改为空。
3. 用while对p进行判断，非空执行增加头节点的操作，注意保存p->next，每次循环结束之后将p的值改为p->next。
4. 返回头。

原理为遍历链表，不断添加头节点。
#### 📌递归
递归比较难理解，也比较难以叙述，参照代码，将运行过程在纸上写一下。
## 3.代码
```c
struct ListNode * reverseList(struct ListNode *head){
  if(head==NULL)
    return head;
  struct ListNode *p=head->next;  //不用开辟空间
  head->next=NULL;
  while(p){
    struct ListNode*temp=p->next; //暂存
    p->next=head;
    head=p;
    p=temp;
  }
  return head;
}

//递归
struct ListNode *reverseList(struct ListNode *head){
  if(head==NULL || head->next==NULL)
    return head;  //递归写法不能像迭代一样只考虑head=0
  struct ListNode *p=head->next;
  head->next=NULL;
  struct ListNode *newhead=reverseList(p);  //目的是制造最终的头
  p->next=head; //链接,因为p值不变，该语句将节点链接了起来
  return newhead;
}
```
