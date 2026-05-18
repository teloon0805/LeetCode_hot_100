# LeetCode_hot_100
LeetCode Top 100 Algorithm Problems Explained

## 1. 两数之和 (Two Sum)

### 题目描述
给定一个整数数组nums和一个整数目标值target，请你在该数组中找出和为目标值target 的那两个整数，并返回它们的数组下标。
你可以假设每种输入只会对应一个答案，并且你不能使用两次相同的元素。
你可以按任意顺序返回答案。


---

### 解题思路

这里记录了两种解法，展现从基础思路到进阶优化的过程。

#### 方法一：暴力枚举 (Brute Force)
* **思路**：最直观的方法。使用双层 `for` 循环遍历整个数组。外层循环固定一个数字 `nums[i]`，内层循环在它之后的元素中寻找是否存在一个数 `nums[j]`，使得两数之和等于 `target`。
* **评价**：虽然容易想到且不需要额外的空间，但时间效率较低。

#### 方法二：哈希表 (Hash Map) - 🌟 推荐解法
* **思路**：为了把时间复杂度降下来，我们可以“以空间换时间”。在遍历数组时，我们使用一个哈希表（C++ 中的 `std::unordered_map`）来记录**已经遍历过的数字及其对应的下标**。
* 每次遇到一个新数字 `nums[i]`，我们先计算出它需要的“另一半”：`complement = target - nums[i]`。
* 然后我们去哈希表里查一下，这个 `complement` 之前有没有出现过？
    * 如果出现过，直接返回当前下标 `i` 和 `complement` 在哈希表里记录的下标，游戏结束。
    * 如果没有出现过，就把当前的 `nums[i]` 和下标 `i` 存入哈希表，留给后面的数字去匹配。

---

### 代码实现 (C++)

#### 方法一：暴力枚举代码
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int len = nums.size();
        for (int i = 0; i < len - 1; i++) {
            for (int j = i + 1; j < len; j++) {
                if (nums[i] + nums[j] == target) {
                    return {i, j};
                }
            }
        }
        return {}; 
    }
};
