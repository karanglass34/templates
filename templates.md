Certainly! Here are 10 Java templates that follow common patterns for solving a wide range of LeetCode problems:

Two Pointers:
java
Copy code
class Solution {
    public int solveProblem(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        
        while (left < right) {
            // Perform operations based on the problem requirements
        }
        
        // Return the result
    }
}
Sliding Window:
java
Copy code
class Solution {
    public int solveProblem(int[] nums, int k) {
        int left = 0;
        int right = 0;
        int sum = 0;
        int result = Integer.MIN_VALUE;
        
        while (right < nums.length) {
            // Expand the window
            sum += nums[right];
            
            while (/* Check for window constraint */) {
                // Update the result based on the problem requirements
                
                // Shrink the window
                sum -= nums[left];
                left++;
            }
            
            right++;
        }
        
        // Return the result
    }
}
Depth-First Search (DFS):
java
Copy code
class Solution {
    public void dfs(TreeNode node) {
        if (node == null) {
            return;
        }
        
        // Perform operations on the current node
        
        dfs(node.left);
        dfs(node.right);
    }
}
Breadth-First Search (BFS):
java
Copy code
class Solution {
    public void bfs(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                
                // Perform operations on the current node
                
                if (node.left != null) {
                    queue.offer(node.left);
                }
                
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
        }
    }
}
Binary Search:
java
Copy code
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return -1; // If the target is not found
    }
}
Dynamic Programming:
java
Copy code
class Solution {
    public int solveProblem(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        
        // Initialize the base cases
        
        for (int i = 1; i < n; i++) {
            // Compute the current state based on the previous states
        }
        
        return dp[n - 1]; // Return the final result
    }
}
Backtracking:
java
Copy code
class Solution {
    public void backtrack(int[] nums, List<Integer> tempList, List<List<Integer>> result) {
        if (tempList.size() == nums.length) {
            result.add(new ArrayList<>(tempList));
        } else {
            for (int i = 0; i < nums.length; i++) {
                if (/* Check for constraints */) {
                    tempList.add(nums[i]);
                    backtrack(nums, tempList, result);
                    tempList.remove(tempList.size() - 1);
                }
            }
        }
    }
}
``



