# Algorithms -- Recursion


# Ideas

## Recursion

- [What important is, __NEVER JUMP INTO RECURSION.__](https://medium.com/@daniel.oliver.king/getting-started-with-recursion-f89f57c5b60e)

### 1. Recursion in List

1. __Figure out what does your Function proceedure with, what kind of value will it return.__

2. Consider about the __Base-Case__, with which we can end the recursion

3. Deal with the rest part ( beyond the Base-Case ) recursively by using your Function.

4. Proceedure the Details of Base-Case.


#### 1.1. Reverse a complete-List

```C++

listNode* reverse(ListNode* head){

// Base-Case 

    if(head -> next == NULL)
        return head; // With Nothing to do, because it's a single-element List.
    

    listNode* last = reverse(head -> next);

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
    Here we consider about the Situation by sub-List([head->next, end]).
    For this sub-List we begin with m-1, the length we need to proceedure is n - 1.
    */

    head -> next = reverseMN(head -> next, m - 1, n - 1);

    return head;
}

```

#### 1.4 Reverse a List in K-elements Group

1. Reverse a List in Iteration:

```C++

listNode* reverse_Iteration(listNode* head){
    
    listNode* prev, cur, nxt;
    cur = nxt = head;
    prev = NULL;

    while(cur != NULL){
        
    // For given-Node case, we modify the loop:
    // while(cur != givenNode)

        nxt = cur -> next;
        cur -> next = prev;
        prev = cur;
        cur = nxt;

    }

    return prev;
}

```

2. Reverse a List in K-elements Group

```C++

listNode* reverseKGroup(listNode* head, int k){

    if(head == NULL)
        return head;

    listNode* b;
    b = head;

    for(int i = 0; i < k; i++){
        
        if(b == NULL)
            return head;    
        
        b = b -> next;
    }

    listNode* newHead = reverse_givenNode(head, b);
    
    head -> next = reverseKGroup(b, k);

    return newHead;

}

```
