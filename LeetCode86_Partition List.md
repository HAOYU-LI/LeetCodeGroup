# Partition List

---

## Description

---

Given a linked list and a value *x*, partition it such that all nodes less than *x* come before nodes greater than or equal to *x*.

You should preserve the original relative order of the nodes in each of the two partitions.

**Example:**

```bash
Input: head = 1->4->3->2->5->2, x = 3
Output: 1->2->2->4->3->5
```



## Solution

---

将链表分成两个部分，分别是小于x的和大于等于x的。这两个部分的头节点都不一定非NULL，考虑使用两个dummy节点(dummyLeft & dummyRight), 分别用于保存两部分链表。在遍历原来的链表并且构建完两部分链表后，需要连接两部分链表得到结果，所以还需要保存两个链表的头(这里使用left_head & right_head)。

**需要注意的是，有可能右部分的尾节点和左部分的头节点是相邻的，所以在连接之前需要将其断开，也就是将dummyRight->next设为NULL。**

## Complexity

---

只需要遍历一遍链表，所以复杂度为O(n)

## Code(C++)

---

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* partition(ListNode* head, int x) {
        if (!head) { return head;}
        
        ListNode* dummyLeft = new ListNode(0);
        ListNode* dummyRight = new ListNode(0);
        ListNode* left_head = dummyLeft;
        ListNode* right_head = dummyRight;
        ListNode* cur_ptr = head;
        while (cur_ptr != NULL) {
            if (cur_ptr->val < x) {
                dummyLeft->next = cur_ptr;
                dummyLeft = dummyLeft->next;
            } else {
                dummyRight->next = cur_ptr;
                dummyRight = dummyRight->next;
            }
            cur_ptr = cur_ptr->next;
        }
        
        dummyRight->next = NULL; // Attention! Make sure there is no cycle in the list
        dummyLeft->next = right_head->next;
        
        return left_head->next;
    }
};
```

