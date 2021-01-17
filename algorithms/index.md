# Algorithms -- Recursion


# Ideas

## Recursion

### 1. Recursion in List

#### 1.1. Reverse a complete-List

- [What important is, __NEVER JUMP INTO RECURSION: TRUST IT, INSTEAD.__](https://medium.com/@daniel.oliver.king/getting-started-with-recursion-f89f57c5b60e)

```C++

listNode* reverse(ListNode* head){

    /*Base-Case, with wich we can jump out from the recursion*/
    if(head -> next == NULL)
        return head; // With Nothing to do, because it's a single-element List.
    
    /*Deal with the rest part recursively.*/
    listNode* last = reverse(head -> next);

    /*After the Process of the rest part, we have to proceed with the Begining-Case*/
    head -> next -> next = head;
    head -> next = NULL;

    return last;
}



```

#### 1.2 Reverse the first n-element in a List

```C++

listNode* successor = NULL;

listNode* reverseN(listNode* head, int n){

    if(n == 1){
        successor = head.next;
        return head;
    }

    listNode* last = reverseN(head -> next, n - 1);

    head -> next = successor;
    head -> next -> next = head;

    return last;
}

```

#### 1.3 Reverse the [m, n] elements in a List

```C++

listNode* reverseMN(listNode *head, int m, int n){
    
    if(m == 1)
        return reverseN(head, n);
    /*
    如果 m != 1 怎么办？如果我们把 head 的索引视为 1，那么我们是想从第 m 个元素开始反转对吧；
    如果把 head.next 的索引视为 1 呢？那么相对于 head.next，反转的区间应该是从第 m - 1 个元素开始的；
    那么对于 head.next.next 呢……
    */
    head -> next = reverseMN(head -> next, m - 1, n - 1);

    return head;
}

```

#### 1.4 Reverse a List in K-elements Group

- Reverse a List in Iteration:

```C++

listNode* reverse_Iteration(listNode* head){
    
    listNode* prev, cur;
    cur = head;
    prev = NULL;

    while(cur != NULL){
        cur -> next = prev;
        prev = cur;
        cur = cur.next;
    }

    return prev;
}

```
