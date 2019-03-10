---
layout: page
title: 刷题
description:
---
## 目录
* [分治法](#分治法)
    * [二分查找](#二分查找)
    * [最小的K个数](#最小的K个数)
* [树](#树)
    * [遍历](#遍历)
      * [前中后](#前中后)
      * [层序](#层序)

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
#### [最小的K个数](https://www.nowcoder.com/practice/6a296eb82cf844ca8539b57c23e6e9bf?tpId=13&tqId=11182&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
快排
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
堆排序
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
### 树
#### [遍历](https://leetcode.com/problems/binary-tree-preorder-traversal/)
##### 前中后
递归
```
void preorder(TreeNode* root,vector<int> &result)
{
   if(root == NULL)
   {
      return ;
   }
   result.push_back(root->val);
   preorder(root->left,result);
   preorder(root->right,result);
}

vector<int> preorderTraversal(TreeNode* root) {
   vector<int> result;
   if(root == NULL)
   {
      return result;
   }
   preorder(root,result);
   return result;
}
```
非递归(后序反转实现)
```
vector<int> preorderTraversal(TreeNode* root) {
   vector<int> result;
   if(root == NULL)
   {
      return result;
   }
   stack<TreeNode*> visited;
   TreeNode* visiting = root;
   while(visiting!=NULL || !visited.empty())
   {
      if(visiting!=NULL)
      {
          visited.push(visiting);
          result.push_back(visiting->val);
          visiting = visiting->left;
      }else{
          visiting = visited.top();
          visited.pop();
          visiting = visiting->right;
      }
   }
   return result;
}
```
##### 层序
```
vector<int> PrintFromTopToBottom(TreeNode* root) {
   queue<TreeNode*> q;
   vector<int> result;
   if (root == NULL)
   {
      return result;
   }
   q.push(root);
   while(!q.empty())
   {
      TreeNode* node = q.front();
      if(node->left!=NULL){
         q.push(node->left);
      }
      if(node->right!=NULL){
         q.push(node->right);
      }
      result.push_back(node->val);
      q.pop();
   }
   return result;
}
```
