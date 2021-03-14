# Algorithms Devide and Conquer


# Algorithms: Devide and Conquer

![DC](/dinive-conquer-algorithm-1-638.jpg)

## Traverse vs. Divide & Conquer

- both Recursive

- __Result in Parameter vs. Result in return Value__

- __Top-down vs. Bottom-up__

## Basic Usage

- Merge Sort / Quick Sort

- Almost 90% Binary Tree Problems

## Merge Sort & Quick Sort

- Merge Sort

- Quick Sort

## Exercises on LeetCode

- [LeetCode 104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

    - Divide & Conquer

        ```java
        class Solution {
            // Divide & Conquer
            public int maxDepth(TreeNode root) {
                if(root == null)
                    return 0;
                
                int left = maxDepth(root.left);
                int right = maxDepth(root.right);
                
                return Math.max(left, right) + 1; 
            }
        }
        ```

    - Recursion

        ```java
        class Solution {

            private int depth = 0;
            
            public int maxDepth(TreeNode root) {
                if(root == null)
                    return depth;
    
                traverse(root, 1); 
                return depth; 
            }
            
            private void traverse(TreeNode root, int curdepth){
                if(root == null)
                    return;

                if(curdepth > depth)
                    depth = curdepth;

                traverse(root.left, curdepth + 1);
                traverse(root.right, curdepth + 1);
                return;
            }
        }
        ```

- [LeetCode 110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

    - with Help of `maxDepth`
    
        ```java
        class Solution {
            public boolean isBalanced(TreeNode root) {
                if(root == null)
                    return true;
                
                int ldepth = depth(root.left);
                int rdepth = depth(root.right);
                if(Math.abs(ldepth - rdepth) > 1)
                    return false;
                return isBalanced(root.left) && isBalanced(root.right);
                
            }
            
            private int depth(TreeNode root){
                if(root == null)
                    return 0;
                int left = depth(root.left);
                int right = depth(root.right);
                
                return 1 + Math.max(left, right);
            }
        }
        ```
    
    - Divide & Conquer ( Master it! )
        
        ```java
        class ResultType{
            public boolean isBalanced;
            public int maxDepth;
            public ResultType(boolean isBalanced, int maxDepth){
                this.isBalanced = isBalanced;
                this.maxDepth = maxDepth;
            }
        }

        class Solution {
            public boolean isBalanced(TreeNode root) {
                return helper(root).isBalanced;
                
            }
            
            private ResultType helper(TreeNode root){
                
                if(root == null)
                    return new ResultType(true, 0);
                
                ResultType left = helper(root.left);
                ResultType right = helper(root.right);
                
                if(!left.isBalanced || !right.isBalanced)
                    return new ResultType(false, -1);
                if(Math.abs(left.maxDepth - right.maxDepth) > 1)
                    return new ResultType(false, -1);
                
                return new ResultType(true, Math.max(left.maxDepth, right.maxDepth) + 1);
            }
        }
        ```

- [LeetCode 124. Binary Tree Maximum Path Sum (HARD)](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

    ```java
    private class ResultType{
            int singlePath, maxPath;
            // singlePath: from root to bottom, can include no Node
            // maxPath: maximum Path from any Node in Tree, 
            // include at least 1 Node
            ResultType(int singlePath, int maxPath){
                this.singlePath = singlePath;
                this.maxPath = maxPath;
            }
        }

    class Solution {
    
        private ResultType helper(TreeNode root){
            if(root == null)
                return new ResultType(0, Integer.MIN_VALUE);

            // Divide
            ResultType left = helper(root.left);
            ResultType right = helper(root.right);
            
            // Conquer
            int singlePath = Math.max(left.singlePath, right.singlePath) + root.val;
            singlePath = Math.max(singlePath, 0);
            
            int maxPath = Math.max(left.maxPath, right.maxPath);
            maxPath = Math.max(maxPath, left.singlePath + right.singlePath + root.val);
            
            return new ResultType(singlePath, maxPath);
        }
        
        public int maxPathSum(TreeNode root) {
            ResultType result = helper(root);
            return result.maxPath;
        }
    }
    ```

- [LeetCode 144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)

    - Recursion -- __DONNOT JUMP INTO RECURSION!__
        ```java
        class Solution {
            // Recursion
            public List<Integer> preorderTraversal(TreeNode root) {   
                List<Integer> result = new ArrayList<Integer>();
                traverse(root, result);
                return result;   
            }

            private void tarverse(TreeNode root, List<Integer> result){   
                if(root == null)
                    return;
                
                result.add(root.val);
                traverse(root.left, result);
                traverse(root.right, result);
            }
        }
        ```

    - Iterative

        ```java
        class Solution {
            // Iterative
            public List<Integer> preorderTraversal(TreeNode root) {
                
                List<Integer> result = new ArrayList<Integer>();
                Stack<TreeNode> stack = new Stack<TreeNode>();
                
                if(root == null)
                    return result;
                
                stack.push(root);
                while(!stack.empty()){
                    TreeNode curr = stack.pop();
                    result.add(curr.val);
                    // Here we must push right first, then left
                    if(curr.right != null)
                        stack.push(curr.right);
                    // Because Stack is a FILO Data Structure
                    if(curr.left != null)
                        stack.push(curr.left);
                }

                return result;
                
            }
        }
        ```
    - Divide and Conquer
    
        ```java
        class Solution {
            // Divide and Conquer
            public List<Integer> preorderTraversal(TreeNode root) {
                
                List<Integer> result = new ArrayList<Integer>();
                
                if(root == null)
                    return result;
                
                // Divide
                List<Integer> left = preorderTraversal(root.left);
                List<Integer> right = preorderTraversal(root.right);

                // Conquer
                result.add(root.val);
                result.addAll(left);
                result.addAll(right);

                return result;
                
            }
        }
        ```

- [LeetCode 236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

    ```java
    class Solution {
        public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
            
            if(root == null || root == p || root == q)
                return root;
            
            //Divide
            TreeNode left = lowestCommonAncestor(root.left, p, q);
            TreeNode right = lowestCommonAncestor(root.right, p, q);

            //Conquer
            if(left != null && right != null)
                return root;
            if(left != null)
                return left;
            if(right != null)
                return right;
            
            return null;
        }
    }
    ```

## BFS in Binary Tree

1. 2 Queues

    - 2 Queues represent different Layers.

2. 1 Queue + 1 Dummy Root

    - Dummy Node represents the End of each Layer.

3. 1 Queue ( BEST )

    - [LeetCode 102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

        - BFS

            ```java
            class Solution {
                public List<List<Integer>> levelOrder(TreeNode root) {
                    List result = new ArrayList();
                    if(root == null)
                        return result;
                    
                    Queue<TreeNode> queue = new LinkedList<TreeNode>();
                    queue.offer(root);
                    
                    while(!queue.isEmpty()){
                        List<Integer> level = new ArrayList<Integer>();
                        int size = queue.size();
                        
                        for(int i = 0; i < size; i++){
                            TreeNode head = queue.poll();
                            level.add(head.val);
                            if(head.left!= null)
                                queue.offer(head.left);
                            if(head.right != null)
                                queue.offer(head.right);
                        }
                        result.add(level);
                    }
                    
                    return result;
                    
                }
            }
            ```

        - DFS ( Understand it )

            ```java
            class Solution {
                public List<List<Integer>> levelOrder(TreeNode root) {
                    
                    List<List<Integer>> results = new ArrayList<List<Integer>>();
                    if(root == null)
                        return results;
                    
                    int maxLevel = 0;
                    while(true){
                        
                        ArrayList<Integer> level = new ArrayList<Integer>();
                        dfs(root, level, 0, maxLevel);
                        
                        if(level.size() == 0)
                            break;
                        
                        results.add(level);
                        maxLevel++;
                    }
                    
                    return results;
                    
                }
                
                private void dfs(TreeNode root, ArrayList<Integer> level, int curtLevel, int maxLevel){
                    if(root == null || curtLevel > maxLevel)
                        return;
                    
                    if(curtLevel == maxLevel){
                        level.add(root.val);
                        return;
                    }
                    
                    dfs(root.left, level, curtLevel + 1, maxLevel);
                    dfs(root.right, level, curtLevel + 1, maxLevel);
                }
            }
            ```

    - [LeetCode 173. Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator/)

        ```java
        class BSTIterator {

            private Stack<TreeNode> stack = new Stack<>();
            private TreeNode curt;
            
            public BSTIterator(TreeNode root) {
                curt = root;
            }
            
            public int next() {
                while(curt != null){
                    stack.push(curt);
                    curt = curt.left;
                }
                
                curt = stack.pop();
                TreeNode node = curt;
                curt = curt.right;
                
                return node.val;
            }
            
            public boolean hasNext() {
                return (curt != null || !stack.isEmpty());
            }
        }
        ```

## Valid BST

- [LeetCode 98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

    - Recursion

        ```java
        class Solution {
            // Inorder Traverse of BST, it ascends.
            private int lastVal = Integer.MIN_VALUE;
            private boolean firstNode = true;
            
            public boolean isValidBST(TreeNode root) {
                if(root == null)
                    return true;
                if(!isValidBST(root.left))
                    return false;
                if(!firstNode && lastVal >= root.val)
                    return false;
                
                firstNode = false;
                lastVal = root.val;
                
                if(!isValidBST(root.right))
                    return false;
                
                return true;
                
            }
        }
        ```

    - Divide & Conquer

        ```java
        class ResultType{
            boolean is_bst;
            int maxValue, minValue;
            public ResultType(boolean is_bst, int maxValue, int minValue){
                this.is_bst = is_bst;
                this.maxValue = maxValue;
                this.minValue = minValue;
            }
        }

        class Solution {
            public boolean isValidBST(TreeNode root) {
                ResultType r = validateHelper(root);
                return r.is_bst;
            }
            
            private ResultType validateHelper(TreeNode root){
                if(root == null)
                    return new ResultType(true, Integer.MIN_VALUE, Integer.MAX_VALUE);
                
                ResultType left = validateHelper(root.left);
                ResultType right = validateHelper(root.right);
                
                if(!left.is_bst || !right.is_bst)
                    return new ResultType(false, 0, 0);
                
                
                if(root.left != null && left.maxValue >= root.val || root.right != null && right.minValue <= root.val)
                    // BST Feature
                    // left child < root
                    // right chile > root
                    return new ResultType(false, 0, 0);
                
                return new ResultType(true, Math.max(root.val, right.maxValue), Math.min(root.val, left.minValue));
                
            }
        }
        ```
