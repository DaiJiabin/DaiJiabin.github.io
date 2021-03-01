# LeetCode

# Go Through LeetCode

![LeetCode](/Leetcode.jpg)

## Recursion / Binary Tree

### 112. Path Sum - simple recursion

- Discription:
  
  - Given the root of a binary tree and an integer targetSum, return true if the tree has a root-to-leaf path such that adding up all the values along the path equals targetSum.

  - A leaf is a node with no children.

- __Idea:__

    1. What kind of traverse should we use? --> Preorder ( why? )
    
    2. What's the Base-Case and what's the Task for every single TreeNode?

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool hasPathSum(TreeNode* root, int targetSum) {
        
        if(root == NULL)
            return false;
        
        if(targetSum == root -> val && root -> left == NULL && root -> right == NULL)
            return true;
        
        targetSum -= root -> val;
        bool left = hasPathSum(root -> left, targetSum);
        bool right = hasPathSum(root -> right, targetSum);
        
        return left || right;
    }
};
```

### 230. Kth Smallest Element in a BST

- Discription:

    - Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

- __Idea:__

  1. What's the Defination / Features of BST?
  
  2. What kind of traverse should we use? --> Inorder ( why? ) 

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    // The most simple Resolution: Serealize the BST and push every element into a vector.
    // Return the k-1th element ( Vector besgins with 0 ).
    vector<int> nums;
    int kthSmallest(TreeNode* root, int k) {
        traverse(nums, root);
        // traverse(root, k);
        return nums[k-1];
    }
    
    void traverse_withVector(vector<int> &nums, TreeNode* root){
        if(root == NULL)
            return;
        else{
            traverse(nums, root -> left);
            nums.push_back(root -> val);
            traverse(nums, root -> right);
        }
    }

    // Without Vector, use Recursion only.
    int count = 0;
    int result;
    void traverse(TreeNode* root, int k){
        if(root == NULL)
            return;
        
        traverse(root -> left, k);
        
        count++;
        if(count == k){
            result = root -> val;
            return;
        }

        traverse(root -> right, k);
    }
};
```

### 538. Convert BST to Greater Tree

- Discription:

    - Given the root of a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus sum of all keys greater than the original key in BST.

    - As a reminder, a binary search tree is a tree that satisfies these constraints:

    - The left subtree of a node contains only nodes with keys less than the node's key.

    - The right subtree of a node contains only nodes with keys greater than the node's key.
    
    - Both the left and right subtrees must also be binary search trees.

- __Idea:__

    1. What kind of traverse should we use? --> Inorder ( why? )
    
    2. What's the Base-Case and what's the Task for every single TreeNode?

```C++
class Solution {
public:
    int sum = 0;
    TreeNode* convertBST(TreeNode* root) {
        if(root == NULL)
            return root;
        
        root -> right = convertBST(root -> right);
        
        root -> val += sum;
        sum = root -> val;
        
        root -> left = convertBST(root -> left);
        return root;
    }
};
```

### 652. Find Duplicate Subtrees - hash table, serealization

- Discription:
  
  - Given the root of a binary tree, return all duplicate subtrees.

  - For each kind of duplicate subtrees, you only need to return the root node of any one of them.

  - Two trees are duplicate if they have the same structure with the same node values.

- __Idea:__

    1. What kind of traverse should we use? --> Postorder ( why? )
    
    2. How to compare subtrees that come from different roots? --> Serealize the subtree to a String and store them into a Hash table ( unordered_map in C++).

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    unordered_map<string, int> memo;
    vector<TreeNode*> res;
    vector<TreeNode*> findDuplicateSubtrees(TreeNode* root) {
        traverse(root, res);
        return res;
    }
    string traverse(TreeNode* root, vector<TreeNode*>& res){
        if(root == NULL)
            return "#";
        string left = traverse(root -> left, res);
        string right = traverse(root -> right, res);
        string result = left + ',' + right + ',' + to_string(root -> val); 
        
        if(memo.find(result) == memo.end())
            memo[result]++;
        else if(memo[result] == 1){
            memo[result]++;
            res.push_back(root);
        }
        else
            memo[result]++;
        
        return result;
    }
    
};
```







- Discription:

- __Idea:__

```C++



```
## Linked List

### 19. Remove Nth Node From End of List ( Middle )

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    
    private ListNode myFunc(ListNode head, int n){
        
        ListNode slow = head, fast = head;
        
        while(n > 0){
            fast = fast.next;
            n--;
        }
        
        if(fast == null)
            return head.next;
        
        while(fast.next != null){
            slow = slow .next;
            fast = fast.next;
        }
        
        slow.next = slow.next.next;
        return head;
    }
    
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if(head == null)
            return head;
        head = myFunc(head, n);
        return head;
    }
}
```

### 141. Linked List Cycle ( Easy ) ( -> HashSet? ) 

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        
        if(head == null || head.next == null)
            return false;
        
        ListNode slow = head, fast = head;
        
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
            if(slow == fast)
                return true;
        }
        
        return false;
        
    }
}
```

### 149. Reorder List ( Middle )

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    
    private ListNode reverse(ListNode head){
        // Reverse a List.
        if(head == null || head.next == null)
            return head;
        
        ListNode retNode = null;
        
        while(head != null){
            ListNode nxt = head.next;
            head.next = retNode;
            retNode = head;
            head = nxt;
        }
        
        return retNode;
    }
    
    
    private ListNode findMid(ListNode head){
        // Find the Middle Node of a List ( slow - fast )
        ListNode slow = head, fast = head.next;
        
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        
        return slow;
    }
    
    private ListNode merge(ListNode left, ListNode right){
        // Merge 2 List. Here we use "index" to decide which List-Node to be chosen.
        // When we merge a list ascend, we can compare the Values of Nodes.
        ListNode retNode = new ListNode(-1);
        ListNode temp = retNode;
        int index = 0;
        
        while(left != null && right != null){
            
            if(index % 2 == 0){
                temp.next = left;
                left = left.next;
            }
            else if(index % 2 == 1){
                temp.next = right;
                right = right.next;
            }
            
            temp = temp.next;
            index++;
            
        }
        
        
        if(left != null)
            temp.next = left;
        else
            temp.next = right;
        
        return retNode.next;
        
    }
    
    public void reorderList(ListNode head) {
        
        if(head == null || head.next == null)
            return;
        
        ListNode midNode = findMid(head);
        
        ListNode left = head;
        ListNode right = reverse(midNode.next);
        midNode.next = null;
        
        ListNode retNode = merge(left, right);
        
        head = retNode;
        return;
    }
}
```
