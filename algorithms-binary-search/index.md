# Algorithms: Binary Search


# Algorithms: Binary Search

![BS](/BS.jpeg)

## Highlight of BS

- with the Judge-setence `if` we can transform a Problem from `O(n)` to `O(n / 2)`

## 4 Points

1. The Thought is to shrank Array `nums` into 2 Numbers -> `while-loop` with `start + 1 < end`

2. update `mid` -> `mid = start + (end - start) / 2`

3. don't be lazy: 3 case -> `==, < , >`

4. at the End ->  `nums[start] / nums[end] ? target` ( watch the Sequence of `start` and `end`, see Codes below )

## when it's needed

- Optimize an O(N) Algorithm ( better than O(N) is fast only O(logN) )

- ( rotated ) sorted Array

## Exercises on LeetCode

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

            if(nums[start] == target) // for the first Position, we caompare nums[start] first.
                return start;
            if(nums[end] == traget)
                return end;

            return -1;
        }
    }
    ```

- [LeetCode 33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

    ```java
    class Solution {
        public int search(int[] nums, int target) {
            if(nums == null || nums.length == 0)
                    return 0;
                
            int start = 0, end = nums.length - 1;
            while(start + 1  < end){
                int mid = start + (end - start) / 2;
                if(nums[mid] == target)
                    return mid;
                if(nums[start] < nums[mid]){
                    if(target >= nums[start] && target <= nums[mid])
                        end = mid;
                    else 
                        start = mid;
                }
                else{
                    if(target >= nums[mid] && target <= nums[end])
                        start = mid;
                    else
                        end = mid;
                }
            }

            if(nums[start] == target)
                return start;
            else if(nums[end] == target)
                return end;
            else
                return -1;
        }
    }
    ```

    ![search_in_sorted_rotated_Array](/search_in_sorted_rotated_Array.png)

- [LeetCode 35. Search Insert Position](https://leetcode.com/problems/search-insert-position/submissions/)

    ```java
    class Solution {
        // Idea: find the first Element that >= target.
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

- [LeetCode 153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

    ```java
    class Solution {
        public int findMin(int[] nums) {
            if(nums == null || nums.length == 0)
                return -1;
            int start = 0, end = nums.length - 1;
            int target = nums[end]; //Q: why set target here? why not nums[start]?
            while(start + 1 < end){
                int mid = start + (end - start) / 2;
                if(nums[mid] == target)
                    start = mid;
                else if(nums[mid] < target)
                    end = mid;
                else if(nums[mid] > target)
                    start = mid;
            }

            if(nums[start] <= nums[end])
                return nums[start];
            else
                return nums[end];
        }
    }
    ```
    ![Rotated_Array](/Roatated_Array.png)

- [LeetCode 162. Find Peak Element](https://leetcode.com/problems/find-peak-element/)

    ```java
    class Solution {
        public int findPeakElement(int[] nums) {
            int start = 0, end = nums.length - 1;
            while(start + 1 < end){
                int mid = start + (end - start) / 2;
                if(nums[mid] < nums[mid + 1]) //case 1
                    start = mid;
                else if(nums[mid] < nums[mid - 1]) //case 2
                    end = mid;
                else if(nums[mid] > nums[mid - 1] && nums[mid] > nums[mid + 1]) //case 3
                    return mid;
                else //case 4
                    start = mid; // `end = mid;` works, too
            }
            if(nums[start] < nums[end])
                return end;
            else
                return start;
        }
    }
    ```

    ![Find_Peak](/Find_Peak.png)

- [LeetCode 278. First Bad Version](https://leetcode.com/problems/first-bad-version/)

    ```java
    public class Solution extends VersionControl {
        public int firstBadVersion(int n) {
            if(n == 0)
                return -1;
            int start = 0, end = n;
            while(start + 1 < end){
                int mid = start + (end - start) / 2;
                if(isBadVersion(mid))
                    end = mid;
                else if(!isBadVersion(mid))
                    start = mid;
            }
            if(isBadVersion(start))
                return start;
            else
                return end;
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
            
            if(nums[end] == traget) // for the last Position, we caompare nums[end] first.
                return end; // an Example, nums = {2, 2, 2}, target = 2.
            if(nums[start] == target)
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
            
            while(start + 1 < end){
                long mid = start + (end - start) / 2;
                if(mid * mid == x)
                    start = mid;
                else if(mid * mid > x)
                    end = mid;
                else if(mid * mid < x)
                    start = mid;
            }

            if(end * end <= x)
                return (int) end;
            return (int) start;
        }
    }
    ```

- [LeetCode74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)

    ```java
    class Solution {
        // Idea: flatten 2D-Matrix into 1D-Matrix
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

    a not so smart way to solve: row first, column then.

    ```java
    class Solution {
        public boolean searchMatrix(int[][] matrix, int target) {
            if(matrix == null || matrix[0].length == 0)
                return false;
            int row = matrix.length;
            int column = matrix[0].length;
            // find row first
            int start = 0, end = row - 1;
            while(start + 1 < end){
                int mid = start + (end - start) / 2;
                if(matrix[mid][0] == target)
                    return true;
                else if(matrix[mid][0] < target)
                    start = mid;
                else if(matrix[mid][0] > target)
                    end = mid;
            }
            // WATCH OUT
            if(matrix[end][0] <= target)
                row = end;
            else if(matrix[start][0] <= target)
                row = start;
            else
                return false;
            
            start = 0;
            end = column - 1;
            
            while(start + 1 < end){
                int mid = start + (end - start) / 2;
                if(matrix[row][mid] == target)
                    return true;
                else if(matrix[row][mid] < target)
                    start = mid;
                else
                    end = mid;
            }
            
            if(matrix[row][start] == target)
                return true;
            else if(matrix[row][end] == target)
                return true;
            else
                return false;
        }
    }
    ```

### Find Any Position

- Find and return, just do it:)
