# Algorithms -- Recursion


![Recursion](/recursion.png)

# Ideas

## Recursion

- [What important is, __NEVER JUMP INTO RECURSION.__](https://medium.com/@daniel.oliver.king/getting-started-with-recursion-f89f57c5b60e)

- Actually... If it's possible, you can jump into it... (Well... You can take a try:) )

- In a Word, what the Blog above says, is that you must make sure that you know the very Defination of your Recursion Function, and trust that it can finish its Work perfectly.

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

#### 1.5 Reverse a List in K-elements Group

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

### 2. Recursion in Binary Tree

- __What kind of order should be used, must know.__

#### 2.1 Traverse - preorder, inorder, postorder

```C++
void traverse(TreeNode* root){
    // Base-case
    if(root == NULL)
        return;

    cout << root -> val; // Preorder
    traverse(root -> left);
    cout << root -> val; // Inorder
    traverse(root -> right);
    cout << root -> val; // Postorder
}
```

## Sort Algorithms

### Merge-Sort

- Ideas:

- Code:

```java
public class mergeSort{
    
    public static void main(String[] args){
        int[] nums = {9,8,7,6,5,4,3,2,1};
        sort(nums);
        /*
        for(int i = 0; i < nums.length; i++)
            System.out.print(nums[i]);
        */
    }

    private static int[] aux;

    private static void merge(int[] a, int lo, int mid, int hi){

        int i = lo;
        int j = mid + 1;

        for(int k = i; k <= hi; k++)
            aux[k] = a[k];

        for(int k = lo; k <= hi; k++){
            if(i > mid) a[k] = aux[j++];
            else if(j > hi) a[k] = aux[i++];
            else if(aux[j] <= aux[i]) a[k] = aux[j++];
            else a[k] = aux[i++];
        }

    }

    private static void sort(int[] nums, int lo, int hi){
        if(hi <= lo)
            return;
        
        int mid = lo + (hi - lo) / 2;
        sort(nums, lo, mid);
        sort(nums, mid + 1, hi);
        merge(nums, lo, mid, hi);

    }

    private static void sort(int[] a){
        aux = new int[a.length];
        sort(a, 0, a.length - 1);
    }
}
```
