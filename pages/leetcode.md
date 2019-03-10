---
layout: page
title: 刷题
description:
---
### 分治法
#### 二分查找
```
int binarySearch(vector<int> &nums, int target) {
    if (nums.empty()) return -1;
    int left = 0, right = nums.size()-1;
    while(left <= right)
    {
      int middle = left + (right - left )/2;//防止溢出
      if (nums[middle] == target) {
        return middle;
      } else if (nums[middle] > target) {
        right = middle - 1;
      } else {
      left = middle + 1;
      }
    }
    return -1;
}
```
