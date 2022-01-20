---
title: "LeetCode 875. Koko Eating Bananas"
date: 2022-01-20T14:31:15+08:00
draft: false

tags: [LeetCode]
categories: [LeetCode]
---
## 問題描述
### 分類： Medium
### 相關主題： Array、 Binary Search
### Link： https://leetcode.com/problems/koko-eating-bananas/

---

### 題目敘述
Koko loves to eat bananas. There are n piles of bananas, the ith pile has piles[i] bananas. The guards have gone and will come back in h hours.

Koko can decide her bananas-per-hour eating speed of k. Each hour, she chooses some pile of bananas and eats k bananas from that pile. If the pile has less than k bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return the minimum integer k such that she can eat all the bananas within h hours.

### 測資
```
Example 1:
    Input: piles = [3,6,7,11], h = 8
    Output: 4

Example 2:
    Input: piles = [30,11,23,4,20], h = 5
    Output: 30

Example 3:
    Input: piles = [30,11,23,4,20], h = 6
    Output: 23
```

## 解題方法
原本看到題目沒有甚麼解題的想法，去稍微看一下 `Related Topics` 找個提示，看到裡面有 `Binary Search` 的標籤後就稍微有點想法了。
<br><br>

既然它要 `Binary Search`，那其中要調整的值就是題目所求的 `k`(速度)，再來就是去找出調整這個 `k` 方法，這個k值的最小值為1，最大值為陣列中最大的值。

我們可以去拿這個 `k` 去計算出這個 `k` 所需要的時間，若算出來的時間比題目上限要小，可以將吃香蕉的速度放慢，也就是將 `k` 值調小，反之則調大。
<br><br>

在這個題目中，我無意中寫出了有向上取整效果的作法，不過好像只有在正數時才有這個效果。
`(x + y - 1) / y`

### 程式碼
```cpp
class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int h) {
        int left = 1, right=0, mid, eat_time;
        for(auto pile: piles) {
            right = max(right, pile);
        }
        
        while(left < right) {
            mid = (left+right)/2;
            eat_time =  hourForEat(piles, mid);
            if(eat_time > h)
                left = mid+1;
            else
                right = mid;
        }
        
        return right;
    }
    
    int hourForEat(vector<int>& piles, int speed) {
        int hour = 0;
        for(auto pile: piles) {
            hour += (pile+speed-1) / speed;
        }
        
        return hour;
    }
};
```

### 結果
![](https://i.imgur.com/bKeBTZw.png)