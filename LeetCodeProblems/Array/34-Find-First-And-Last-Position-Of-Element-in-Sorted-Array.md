# 34-Find First And Last Position Of Elementin Sorted Array - Medium
**在排序数组中查找元素的第一个和最后一个位置**

给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

你的算法时间复杂度必须是 O(log n) 级别。

如果数组中不存在目标值，返回 [-1, -1]。

**示例:**
```
输入: nums = [5,7,7,8,8,10], target = 8
输出: [3,4]

输入: nums = [5,7,7,8,8,10], target = 6
输出: [-1,-1]
```
**所有可能解法**

- 二分查找，寻找哪个边界主要是看等于给定值的情况，是变动left还是right，变动right找左边界，变动left找右边界。

**CODINNG**

```
class Solution {
    func searchRange(_ nums: [Int], _ target: Int) -> [Int] {
        if 0 == nums.count {
            return [-1, -1]
        }

        var left = 0
        var right = nums.count - 1
        var res = [-1, -1];
        while left < right {
            //中间值偏向于左边，寻找左边界
            let mid = (left + right) / 2
            if nums[mid] < target {
                left = mid + 1
            } else {
                right = mid
            }
        }
        if(nums[left] != target) {
            return res
        } else {
          res[0] = left
        }
        right = nums.count - 1
        while left < right {
            //中间值偏向右边，寻找右边界
            let mid = (left + right) / 2 + 1
            if nums[mid] > target {
                right = mid - 1
            } else {
                left = mid
            }
        }

        res[1] = right

        return res
    }
}
```
