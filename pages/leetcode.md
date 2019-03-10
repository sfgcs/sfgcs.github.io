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
#### 最小的K个数(快排)
```
int partition(vector<int> &input,int l,int r){
    int p = input[l];
    while(l<r){
        while(l<r&&input[r]>=p){
            r--;
        }
        swap(input[l],input[r]);
        while(l<r&&input[l]<=p)
        {
            l++;
        }
        swap(input[l],input[r]);
    }
    return l;
}
vector<int> GetLeastNumbers_Solution(vector<int> input, int k) {
    vector<int> result;
    if(input.empty()|| k<=0 || k > input.size()) return result;
    int l = 0;
    int r = input.size() - 1;
    int index = partition(input,l,r);
    while(index != (k-1) )
    {
      if(index<k-1)
        {
            l = index+1;
            index = partition(input,l,r);

        }
        else
        {
            r = index-1;
            index = partition(input,l,r); 
        }
    }
    for(int i = 0;i<=index;i++)
    {
        result.push_back(input[i]);
    }  
    return result;
}
```
