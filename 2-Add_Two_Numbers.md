# Promble 2 #

## First Passed virsion ##
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