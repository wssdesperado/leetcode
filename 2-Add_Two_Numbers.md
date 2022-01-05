# Promble 2 - Add Two Numbers #

## Original virsion ##
```
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        flag = 0
        isFirstTime = True
        result = ListNode()
        start = ListNode()
        while l1 is not None or l2 is not None:
            if l1 is not None:
                num = flag
                flag = 0
                if l2 is not None:
                    num += l1.val + l2.val
                    flag = int(num / 10)
                    l1 = l1.next
                    l2 = l2.next
                    result.val = num % 10
                    if l1 is not None or l2 is not None:
                        new_node = ListNode()
                        result.next = new_node
                        if isFirstTime is True:
                            start.val = result.val
                            start.next = result.next
                            isFirstTime = False
                        result = new_node
                    else:
                        if flag == 0:
                            if isFirstTime is True:
                                start.val = result.val
                                start.next = result.next
                                isFirstTime = False
                        else:
                            new_node = ListNode()
                            result.next = new_node
                            if isFirstTime is True:
                                start.val = result.val
                                start.next = result.next
                                isFirstTime = False
                            result = new_node
                            result.val = flag
                else:
                    num += l1.val
                    flag = int(num / 10)
                    result.val = num % 10
                    l1 = l1.next
                    if l1 is not None or flag != 0:
                        new_node = ListNode()
                        result.next = new_node
                        if isFirstTime is True:
                            start.val = result.val
                            start.next = result.next
                            isFirstTime = False
                        result = new_node
                        result.val = flag         
            else:
                num = flag
                flag = 0
                num += l2.val
                flag = int(num / 10)
                result.val = num % 10
                l2 = l2.next
                if l2 is not None or flag != 0:
                    new_node = ListNode()
                    result.next = new_node
                    if isFirstTime is True:
                        start.val = result.val
                        start.next = result.next
                        isFirstTime = False
                    result = new_node
                    result.val = flag
        return start
```

Outline:
Determine whether the two linked-lists are empty and the carry.

Improve:
Get the value from two linked-lists, if empty, then consider as 0. In this case, only have to concern the carry.

## Better Solution
```
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        carry = 0
        result_head = ListNode()
        result_tail= result_head
        while l1 or l2:
            num1 = l1.val if l1 else 0
            num2 = l2.val if l2 else 0
            sum = num1 + num2 + carry
            carry = sum // 10
            result_tail.next = ListNode(sum % 10)
            result_tail = result_tail.next
            if l1 is not None:
                l1 = l1.next
            if l2 is not None:
                l2 = l2.next
            # tip 1: an elegant way to deal with carry when both linked-lists are end
            if carry > 0:
                result_tail.next = ListNode(carry)
        # tip 2: return head.next to simplify formatting!
        return result_head.next
```
