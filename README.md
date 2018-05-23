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
 
```

##### 442. 数组中重复的数据
```java  
 
```

##### 448. 找到所有数组中消失的数字
```java  
 
```
## 树

## 动态规划

## 数学
