# Algorithms: Binary Search


# Algorithms: Binary Search

![BS](/BS.jpeg)

## Highlight of BS

- with the Judge-setence `if` we can transform a Problem from `O(n)` to `O(n / 2)`

## find any / first / last Position of the searching-Element

- The Thought is to shrank Array `nums` into 2 Numbers.

### Find the First Position

- `end` to `mid`, if possible, return `start`

    ```java
    class Solution{
        public int BinarySearch(int[] nums, int target){    
            if(nums == null || nums.length == 0)
                return -1;

            int start = 0, end = nums.length - 1;
            
            while(start + 1 < end){// WATCH OUT
                int mid = start + (end - start) / 2;
                if(nums[mid] == target)
                    end = mid; // WATCH OUT
                else if(nums[mid] < target)
                    start = mid;
                else
                    end = mid; // WATCH OUT
            }

            if(nums[start] == target)
                return start;
            if(nums[end] == traget)
                return end;

            return -1;
        }
    }
    ```

- [LeetCode 35. Search Insert Position](https://leetcode.com/problems/search-insert-position/submissions/)

    ```java
    class Solution {
        public int searchInsert(int[] nums, int target) {
            
            if(nums == null || nums.length == 0)
                return 0;
            
            int start = 0, end = nums.length - 1;
            while(start + 1  < end){
                int mid = start + (end - start) / 2;
                if(nums[mid] == target)
                    end = mid;
                else if(nums[mid] < target)
                    start = mid;
                else
                    end = mid;
            }
            
            if(nums[start] >= target)
                return start;
            if(nums[end] >= target)
                return end;
            return nums.length;
        }
    }
    ```

### Find the Last Position

- `start` to `mid`, if possible, return `end`

    ```java
    class Solution{
        public int BinarySearch(int[] nums, int target){    
            if(nums == null || nums.length == 0)
                return -1;

            int start = 0, end = nums.length - 1;
            
            while(start + 1 < end){// WATCH OUT
                int mid = start + (end - start) / 2;
                if(nums[mid] == target)
                    start = mid; // WATCH OUT
                else if(nums[mid] < target)
                    start = mid; // WATCH OUT
                else
                    end = mid;
            }

            if(nums[end] == target)
                return end;
            if(nums[start] == traget)
                return start;

            return -1;
        }
    }
    ```

- [LeetCode 69. Sqrt(x)](https://leetcode.com/problems/sqrtx/)

    ```java
    class Solution {
        public int mySqrt(int x) {
            long start = 1, end = x;
            
            while(start + 1= < end){
                long mid = start + (end - start) / 2;
                if(mid * mid <= x)
                    start = mid;
                else
                    end = mid;
            }

            if(end * end <= x)
                return (int) end;
            return (int) start;
        }
    }
    ```

### Find Any Position

- [LeetCode74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)

    ```java
    class Solution {
        // flatten 2D-Matrix into 1D-Matrix
        public boolean searchMatrix(int[][] matrix, int target) {
            
            if(matrix == null)
                return false;
            
            if(matrix.length == 0 || matrix[0].length == 0)
                return false;
            
            int row = matrix.length, column = matrix[0].length;
            
            int start = 0, end = row * column - 1;
            
            while(start + 1 < end){
                
                int mid = start + (end - start) / 2;
                int now = matrix[mid / column][mid % column];
                if(now == target)
                    return true;
                else if(now < target)
                    start = mid;
                else
                    end = mid;
            }
            
            if(matrix[start / column][start % column] == target)
                return true;
            if(matrix[end / column][end % column] == target)
                return true;
            
            return false;
            
        }
    }
    ```

    a not so smart way to solve:

    ```java

    ```


