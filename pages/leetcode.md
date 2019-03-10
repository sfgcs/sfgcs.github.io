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
#### [最小的K个数(快排)](https://www.nowcoder.com/practice/6a296eb82cf844ca8539b57c23e6e9bf?tpId=13&tqId=11182&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```
int partition(vector<int> &input,int l,int r){
    int p = input[l]; // 最左边当成轴
    while(l<r){
        while(l<r&&input[r]>=p){ //左右不相遇
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
附堆排序代码
```
void adjustHeap(vector<int> &input,int i,int length){
    int child = i*2+1;
    if(child<length)
    {
        if (child+1<length&&input[child+1]<input[child])
        {
            child++;
        }
        if (input[child]<input[i])
        {
            swap(input[i],input[child]);
            adjustHeap(input,child,length);//递归调整
        }
    }
}
vector<int> GetLeastNumbers_Solution(vector<int> input, int k) {
    vector<int> result;
    if(input.empty()|| k<=0 || k > input.size()) return result;
    for (int i = input.size()/2 -1;i >= 0;i--)
    {
        adjustHeap(input,i,input.size()-1);
    }
    for (int i = 0; i < k; ++i)
    {
        result.push_back(input[0]);
        swap(input[0],input[input.size()-i-1]);
        adjustHeap(input,0,input.size()-1-i);
    }
    return result;
}
```
