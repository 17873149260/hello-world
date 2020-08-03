# reverseList

①思路：在链表元素个数>1的情况下，先将链表的前两个结点反转，再将后面剩余的结点逐个添加到首端。

struct ListNode* reverseList(struct ListNode* head)
{
    if (head == NULL || head -> next == NULL)//空链表或只有一个结点的链表
        return head;
    struct ListNode *p = head -> next, *q = head -> next -> next, *t;//q从第3个结点开始，t为q的下一个结点，防止断链

    p -> next = head;
    head -> next = NULL;//将链表的前两个结点反转，为后面在头部逐个添加结点做准备
    while (q)
    {
        t = q -> next; //t指向q的下一个结点
        q -> next = p; //q连上p
        p = q; //p移动到q
        q = t; //q向后移动
    }
    return p;
}

②头插法

struct ListNode* reverseList(struct ListNode* head)
{
    struct ListNode *output=(struct ListNode*)malloc(sizeof(struct ListNode));
    struct ListNode*p=head;struct ListNode*q;struct ListNode*temp;
    output->next=NULL;
    
    while(p!=NULL)
    {
        temp=output->next;
        q=p->next;
        output->next=p;
        p->next=temp;
        p=q;
    }
    return output->next;
}

③递归法

struct ListNode* reverseList(struct ListNode* head)
{
    //当为空或者只有一个节点
    if(!head || !head->next)  return head;
    
    //递归反转head->next
    struct ListNode *res = reverseList(head->next);
    
    //res的尾结点是head->next，所以需要将之前弹出的head接在此结点上
    head->next->next = head;
    head->next = NULL;  //将head结点的next置空
    return res;
}




#Bintree-> list

void flatten（struct TreeNode *根）
{
    while(root)
    {
        if(root->left)
        {
            struct TreeNode * p = root->left;
            while(p->right) 
                p=p->right;

            p->right=root->right;
            root->right=root->left;
            root->left=NULL;
        }
        root=root->right;
    }
}
