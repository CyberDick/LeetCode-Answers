# LeetCode-Answers
记录部分leetcode题解

## 链表类
##### 141. 环形链表
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
        if(head == null || head.next == null){
            return false;
        }
        ListNode slow = head;
        ListNode fast = head.next;
        while(fast != null){
            if(slow == fast){
                return true;
            }
            slow = slow.next;
            fast = fast.next;
            if(fast != null){
                fast = fast.next;
            }
        }
        return false;
    }
}
```

##### 142. 环形链表II
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
    public ListNode detectCycle(ListNode head) {
        if(head == null || head.next == null){
            return null;
        }
        ListNode slow = head;
        ListNode fast = head;
        while(fast != null){
            slow = slow.next;
            fast = fast.next;
            if(fast != null){
                fast = fast.next;
            }
            if(fast == slow){
                while(head != slow){
                    head = head.next;
                    slow = slow.next;
                }
                return head;
            }
        }
        return null;
    }
}

```
##### 160. 相交链表
```java  
 /**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode pa = headA;
        ListNode pb = headB;
        while(pa != pb){
            pa = pa == null ? headB : pa.next;
            pb = pb == null ? headA : pb.next;
        }
        return pa;
    }
}
```

##### 206. 反转链表

解法a
```java  
 /**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }
        ListNode newHead = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return newHead;
    }
}
```
解法b
```java  
 /**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }
        ListNode newHead = null;
        while(head != null){
            ListNode node = head;
            head = head.next;
            node.next = newHead;
            newHead = node;
        }
        return newHead;
    }
}
```
解法c
```java  
 /**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }
        ListNode pre = null;
        ListNode cur = head;
        while(cur != null){
            ListNode next = cur.next;
            cur.next = pre;
            
            pre = cur;
            cur = next;
        }
        return pre;
    }
}
```
##### 234. 回文链表
```java  
 /**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        if(head == null || head.next == null){
            return true;
        }
        ListNode slow = head;
        ListNode fast = head;
        while(fast != null){
            slow = slow.next;
            fast = fast.next;
            if(fast != null){
                fast = fast.next;
            }
        }
        ListNode cur = slow;
        ListNode pre = null;
        while(cur != null){
            ListNode next = cur.next;
            cur.next = pre;
            
            pre = cur;
            cur = next;
        }
        while(pre != null){
            if(pre.val != head.val){
                return false;
            }
            pre = pre.next;
            head = head.next;
        }
        return true;
    }
}
```

## 数组
##### 73. 矩阵置零
```java  
 class Solution {
    public void setZeroes(int[][] matrix) {
        int row = 0;
        int col = 0;
        int m = matrix.length;
        int n = matrix[0].length;
        for(int j = 0 ; j < n ; j++){
            if(matrix[0][j] == 0){
                row = 1;
            }
        }
        for(int i = 0 ; i < m ; i++){
            if(matrix[i][0] == 0){
                col = 1;
            }
        }
        for(int i = 1 ; i < m ; i++){
            for(int j = 1 ; j < n ; j++){
                if(matrix[i][j] == 0){
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }
        for(int i = 1 ; i < m ; i++){
            for(int j = 1 ; j < n ; j++){
                if(matrix[i][0] == 0 || matrix[0][j] == 0){
                    matrix[i][j] = 0;
                }
            }
        }
        if(row == 1){
            for(int j = 0 ; j < n ; j++){
                matrix[0][j] = 0;
            }
        }
        if(col == 1){
            for(int i = 0 ; i < m ; i++){
                matrix[i][0] = 0;
            }
        }
    }
}
```

##### 80. 删除排序数组中的重复项 II
```java  
 class Solution {
    public int removeDuplicates(int[] nums) {
        int n = nums.length;
        if(n == 0){
            return 0;
        }
        int len = 1;
        int pos = 0;
        for(int i = 1 ; i < n ; i++){
            if(nums[i-1] == nums[i]){
                len++;
            }else{
                if(len >= 2){
                    nums[pos++] = nums[i-1];
                    nums[pos++] = nums[i-2];
                }else{
                    nums[pos++] = nums[i-1];
                }
                len = 1;
            }
        }
        if(len >= 2){
            nums[pos++] = nums[n-1];
            nums[pos++] = nums[n-2];
        }else{
            nums[pos++] = nums[n-1];
        }
        return pos;
    }
}
```

##### 169. 求众数
```java  
class Solution {
    public int majorityElement(int[] nums) {
        int n = nums.length;
        int major = nums[0];
        int cnt = 1;
        for(int i = 1 ; i < n ; i++){
            if(cnt == 0){
                major = nums[i];
                cnt = 1;
            }
            else if(major != nums[i]){
                cnt--;
            }
            else if(major == nums[i]){
                cnt++;
            }
        }
        return major;
    }
} 
```

##### 442. 数组中重复的数据
```java  
class Solution {
    public List<Integer> findDuplicates(int[] nums) {
        List<Integer> list = new ArrayList<>();
        for(int i = 0 ; i < nums.length ; i++){
            int index = Math.abs(nums[i])-1;
            nums[index] = -nums[index];
            if(nums[index] > 0){
                list.add(index+1);
            }
        }
        return list;
    }
} 
```

##### 448. 找到所有数组中消失的数字
```java  
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> list = new ArrayList<>();
        int n = nums.length;
        for(int i = 0 ; i < n ; i++){
            int index = (nums[i]-1) % n;
            nums[index] += n;
        }
        for(int i = 0 ; i < n ; i++){
            if(nums[i] < n){
                list.add(i+1);
            }
        }
        return list;
    }
}
```

## 树
##### 103. 二叉树的锯齿形层次遍历
```java  
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> zig = new ArrayList<>();
        if(root == null){
            return zig;
        }
        int dir = 0;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        while(q.size() > 0){
            int size = q.size();
            dir++;
            dir = dir % 2;
            List<Integer> layer = new ArrayList<>();
            while(size > 0){
                TreeNode cur = q.poll();
                layer.add(cur.val);
                if(cur.left != null){
                    q.offer(cur.left);
                }
                if(cur.right != null){
                    q.offer(cur.right);
                }
                size--;
            }
            if(dir == 0){
                Collections.reverse(layer);
            }
            zig.add(layer);
        }
        return zig;
    }
} 
```

##### 105. 从前序与中序遍历序列构造二叉树
```java  
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        int n = preorder.length;
        return helper(preorder,inorder,0,n-1,0,n-1);
    }
    public TreeNode helper(int[] pre,int[] in,int pl,int pr,int il,int ir){
        if(pl > pr){
            return null;
        }
        TreeNode root = new TreeNode(pre[pl]);
        int len = 0;
        for(int i = il ; i <= ir ; i++){
            if(in[i] == pre[pl]){
                break;
            }
            len++;
        }
        root.left = helper(pre,in,pl+1,pl+len,il,il+len-1);
        root.right = helper(pre,in,pl+len+1,pr,il+len+1,ir);
        return root;
    }
}
```
##### 226. 翻转二叉树 
```java  
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root == null){
            return root;
        }
        TreeNode tmp = root.left;
        root.left = root.right;
        root.right = tmp;
        invertTree(root.left);
        invertTree(root.right);
        return root;
    }
}
```

##### 236. 二叉树的最近公共祖先
```java  
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null){
            return root;
        }
        if(p == root || q == root){
            return root;
        }
        TreeNode left = lowestCommonAncestor(root.left,p,q);
        TreeNode right = lowestCommonAncestor(root.right,p,q);
        if(left != null && right != null){
            return root;
        }else if(left != null){
            return left;
        }else if(right != null){
            return right;
        }
        return null;
    }
} 
```

##### 606. 根据二叉树创建字符串
```java  
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public String tree2str(TreeNode t) {
        if(t == null){
            return "";
        }
        StringBuilder sb = new StringBuilder();
        sb.append(t.val);
        if(t.right != null){
            sb.append("(");
            sb.append(tree2str(t.left));
            sb.append(")");
            sb.append("(");
            sb.append(tree2str(t.right));
            sb.append(")");
        }
        else if(t.right == null && t.left != null){
            sb.append("(");
            sb.append(tree2str(t.left));
            sb.append(")");
        }
        return sb.toString();
    }
} 
```

## 动态规划
##### 53. 最大子序和
```java  
class Solution {
    public int maxSubArray(int[] nums) {
        int sum = nums[0];
        int maxSum = nums[0];
        for(int i = 1 ; i < nums.length ; i++){
            sum = Math.max(nums[i], nums[i] + sum);
            maxSum = Math.max(maxSum,sum);
        }
        return maxSum;
    }
} 
```

##### 72. 编辑距离
```java  
class Solution {
    public int minDistance(String w1, String w2) {
        int m = w1.length();
        int n = w2.length();
        int[][] dp = new int[m+1][n+1];
        for(int i = 1 ; i <= m ; i++){
            dp[i][0] = i;
        }
        for(int j = 1 ; j <= n ; j++){
            dp[0][j] = j;
        }
        for(int i = 1 ; i <= m ; i++){
            for(int j = 1 ; j <= n ; j++){
                if(w1.charAt(i-1) == w2.charAt(j-1)){
                    dp[i][j] = dp[i-1][j-1];
                }else{
                    dp[i][j] = Math.min(dp[i-1][j] + 1,dp[i][j-1] + 1);
                    dp[i][j] = Math.min(dp[i][j], dp[i-1][j-1] + 1);
                }
            }
        }
        return dp[m][n];
    }
} 
```

##### 300. 最长上升子序列
解法a
```java  
class Solution {
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        int []a = new int[n];
        int maxlen = 0;
        for(int i = 0 ; i < n ; i++){
            a[i] = 1;
            for(int j = 0 ; j < i ; j++){
                if(nums[i] > nums[j]){
                    a[i] = Math.max(a[i],a[j] + 1);
                }
            }
            maxlen = Math.max(maxlen,a[i]);
        }
        return maxlen;
    }
}
```
解法b
```java  
class Solution {
    public int lengthOfLIS(int[] nums) {
        int []tail = new int[nums.length];
        int size = 0;
        for(int num : nums){
            int i = 0, j = size;
            while(i != j){
                int m = (i+j) / 2;
                if(num > tail[m]){
                    i = m+1;
                }else{
                    j = m;
                }
            }
            tail[i] = num;
            if(i == size)size++;
        }
        return size;
    }
}
```

##### 673. 最长递增子序列的个数
```java  
class Solution {
    public int findNumberOfLIS(int[] nums) {
        int n = nums.length;
        int[] a = new int[n];
        int[] b = new int[n];
        int maxLen = 0;
        int cnt = 0;
        for(int i = 0 ; i < n ; i++){
            a[i] = 1;
            b[i] = 1;
            for(int j = 0 ; j < i ; j++){
                if(nums[i] > nums[j]){
                    if(a[i] < a[j] + 1){
                        a[i] = a[j] + 1;
                        b[i] = b[j];
                    }
                    else if(a[i] == a[j] + 1){
                        b[i] += b[j];
                    }
                }
            }
            if(maxLen == a[i]){
                cnt += b[i];
            }
            else if(maxLen < a[i]){
                maxLen = a[i];
                cnt = b[i];
            }
        }
        return cnt;
    }
}
```

## 数学
##### 50. Pow(x, n)
```java  
class Solution {
    public double myPow(double x, int n) {
        int flag = 0;
        long p = n;
        if(p < 0){
            p = -p;
            flag = 1;
        }
        double res = 1;
        while(p > 0){
            if((p & 0x1) == 1){
                res = res * x;
            }
            x = x * x;
            p = p >> 1;
        }
        return flag == 1 ? 1 / res : res;
    }
} 
```

##### 69. x 的平方根
```java  
class Solution {
    public int mySqrt(int x) {
        double x1 = 1;
        double x2 = 2;
        while(Math.abs(x1 - x2) >= 0.1){
            x2 = x1;
            x1 = (x1 + x/x1)/2;
        }
        return (int)x1;
    }
} 
```

##### 137. 只出现一次的数字 II
解法a
```java  
class Solution {
    public int singleNumber(int[] nums) {
        int single = 0;
        for(int i = 0 ; i < 32 ; i++){
            int bitSum = 0;
            for(int j = 0 ; j < nums.length ; j++){
                bitSum += (nums[j] >> i) & 0x1;
            }
            single |= (bitSum % 3) << i;
        }
        return single;
    }
}
```
解法b
```java  
class Solution {
    public int singleNumber(int[] nums) {
        int one = 0;
        int two = 0;
        for(int i = 0 ; i < nums.length ; i++){
            one = (nums[i]^one) & (~two);
            two = (nums[i]^two) & (~one);
        }
        return one;
    }
} 
```

##### 342. 4的幂
```java  
class Solution {
    public boolean isPowerOfFour(int num) {
        if(num < 0){
            return false;
        }
        if((num & (num - 1)) != 0){
            return false;
        }
        if((num & (0x55555555)) != 0){
            return true;
        }
        return false;
    }
} 
```

##### 367. 有效的完全平方数
解法a
```java  
class Solution {
    public boolean isPerfectSquare(int num) {
        int x = num;
        while(x * x > num){
            x = (x + num / x) >> 1;
        }
        return x * x == num;
    }
}
```
解法b
```java  
class Solution {
    public boolean isPerfectSquare(int num) {
        int i = 1;
        while(num > 0){
            num = num - i;
            i = i + 2;
        }
        return num == 0;
    }
}
```
解法c
```java  
class Solution {
    public boolean isPerfectSquare(int num) {
        long low = 1;
        long high = num;
        while(low <= high){
            long mid = (high - low)/2 + low;
            if(mid * mid == num){
                return true;
            }else if(mid * mid < num){
                low = mid + 1;
            }else{
                high = mid - 1;
            }
        }
        return false;
    }
}
```

