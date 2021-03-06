## 合并K个排序链表
### 题目描述

合并 k 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

示例:
```
输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
```

### 解法
从链表数组索引 0 开始，[合并前后相邻两个有序链表](https://github.com/yanglbme/leetcode/tree/master/solution/021.Merge%20Two%20Sorted%20Lists)，放在后一个链表位置上，依次循环下去...最后 lists[len - 1] 即为合并后的链表。注意处理链表数组元素小于 2 的情况。

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
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }
        
        int len = lists.length;
        if (len == 1) {
            return lists[0];
        }
       
        // 合并前后两个链表，结果放在后一个链表位置上，依次循环下去
        for (int i = 0; i < len - 1; ++i) {
            lists[i + 1] = mergeTwoLists(lists[i], lists[i + 1]);
        }
        return lists[len - 1];
        
    }
    
    /**
     * 合并两个有序链表
     * @param l1 
     * @param l2
     * @return listNode
     */
    private ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }
        if (l1.val < l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        }
        l2.next = mergeTwoLists(l1, l2.next);
        return l2;
    }
}
```