# LeetCode 142. Linked List Cycle II


## 問題描述
### 分類： Easy
### 相關主題： Hash Table、 Linked List、 Two Pointers 
### Link： https://leetcode.com/problems/linked-list-cycle-ii/

---

### 題目敘述
Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return null.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to (0-indexed). It is -1 if there is no cycle. Note that pos is not passed as a parameter.

Do not modify the linked list.

### 測資
![](https://i.imgur.com/PbKbjQh.png)
```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

## 解題方法
### hash table
這題需要我們去找出 `list` 中出現循環的起點，若 `list` 中沒有出現循環，則返回空指標。

最直觀的解法就是去使用 **`hash table`**， 紀錄出現過的 `listNode` 之記憶體位址，若再次出現則為循環的起點。

不過這種做法的缺點是要去記錄所有的 `node`，會使用到較多的空間，速度也較慢。
#### 程式碼
```cpp
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
    ListNode *detectCycle(ListNode *head) {
        unordered_set<ListNode*> seen;
        
        ListNode *node = head;
        while(node != nullptr) {
            if(seen.count(node) == 1)
                return node;
            seen.insert(node);
            node = node->next;
        }
        
        return nullptr;
    }
};
```

#### 結果
![](https://i.imgur.com/C79sgnq.png)

---

### Fast-Slow pointer
這題我們可以使用快慢指標來判斷是否出現循環，並找出循環的起始點。

`Fast pointer` 一次移動兩格; `Slow pointer` 一次移動一格

若他們兩個指標相遇時，表示出現了循環。這時將其中一個指標移到起點，兩個指標每次都只動一格，它們再次相遇時的那個點，就是循環的起始點。

雖然沒有很了解其中的原理，但它就是有這個特殊的性質。

可以從結果中看到，這種解法速度較快，且記憶體使用率也較低。
#### 程式碼
```cpp
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
    ListNode *detectCycle(ListNode *head) {
        ListNode *slow = head;
        ListNode *fast = head;
        
        while(fast && fast->next) {
            fast = fast->next->next;
            slow = slow->next;
            if(fast == slow)
                break;
        }
        if(fast && fast->next) {
            fast = head;
            while(fast != slow) {
                fast = fast->next;
                slow = slow->next;
            }
            return fast;
        }
        return nullptr;
    }
};
```

#### 結果
![](https://i.imgur.com/XQp8HaP.png)
