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
   * [性质判断](#性质判断)
      * [对称](#对称)
      * [子树](#子树)
      * [BST判断](#BST判断)
      * [AVL判断](#AVL判断)
   * [BST](#BST)
      * [BST公共祖先](#BST公共祖先)
      * [转双向链表](#转双向链表)
      * [后序遍历判断](#后序遍历判断)
   * [深度](#深度)
      * [求最大深度](#求最大深度)
   * [路径](#路径)
      * [和为某值的路径](#和为某值的路径)
      * [最大距离](#和为某值的路径)
      * [一般公共祖先](#一般公共祖先)
   * [根据遍历结果反推](#根据遍历结果反推)
      * [重建二叉树](#重建二叉树)

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
#### 性质判断
##### [对称](https://www.nowcoder.com/practice/ff05d44dfdb04e1d83bdbdab320efbcb?tpId=13&tqId=11211&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```
bool isSymmetrical(TreeNode* pRoot)
{
   if (pRoot==NULL) return true;
   return isSymmetrical(pRoot->left,pRoot->right);
}

bool isSymmetrical(TreeNode* left,TreeNode* right)
{
   if (left==NULL&&right==NULL) return true;
   if (left==NULL||right==NULL) return false;
   if (left->val!=right->val) return false;
   return isSymmetrical(left->left,right->right)&&isSymmetrical(left->right,right->left);
}
```
##### [子树](https://www.nowcoder.com/practice/6e196c44c7004d15b1610b9afca8bd88?tpId=13&tqId=11170&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```
bool isSubtree(TreeNode* pRoot1, TreeNode* pRoot2)
{
    if (pRoot2==NULL) return true;
    if (pRoot1==NULL) return false;
    if (pRoot1->val!=pRoot2->val) return false;
    return isSubtree(pRoot1->left,pRoot2->left)&&isSubtree(pRoot1->right,pRoot2->right);
}
bool HasSubtree(TreeNode* pRoot1, TreeNode* pRoot2)
{
    if (pRoot1==NULL||pRoot2==NULL) return false;
    if (pRoot1->val==pRoot2->val)
    {
        return isSubtree(pRoot1,pRoot2)
            ||HasSubtree(pRoot1->left, pRoot2)
            ||HasSubtree(pRoot1->right, pRoot2);
    }
    return false;
}
```
##### [BST判断](https://www.nowcoder.com/practice/6e196c44c7004d15b1610b9afca8bd88?tpId=13&tqId=11170&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```
bool isValidBST(TreeNode* root) {
   if (root==NULL) return true;

   stack<TreeNode*> visited;
   TreeNode* visiting = root;
   TreeNode* last = NULL;
   while(visiting!=NULL||!visited.empty())
   {
      if (visiting!=NULL)
      {
          visited.push(visiting);
          visiting = visiting->left;
      }else{
          visiting = visited.top();
          if(last!=NULL)
          {
            if (visiting->val<=last->val)
            {
                return false;
            }else{
                last = visiting;
            }
          }else{
            last = visiting;
          }
          visited.pop();
          visiting = visiting->right;
      }  
   }
   return true;     
}
```
##### [AVL判断](https://www.nowcoder.com/practice/8b3b95850edb4115918ecebdf1b4d222?tpId=13&tqId=11192&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```
// 可剪枝https://www.nowcoder.com/questionTerminal/8b3b95850edb4115918ecebdf1b4d222
bool IsBalanced_Solution(TreeNode* pRoot) {
  if (pRoot==NULL) return true;
  int left = TreeDepth(pRoot->left);
  int right = TreeDepth(pRoot->right);
  if (left-right>1||right-left>1) return false;
  return IsBalanced_Solution(pRoot->left)&&IsBalanced_Solution(pRoot->right);
}
int TreeDepth(TreeNode* pRoot)
{
  if (pRoot == NULL) return 0;
  return max(1+TreeDepth(pRoot->left),1+TreeDepth(pRoot->right));
}
```
#### BST
##### [BST公共祖先](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree)
```
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
   if (root ==NULL||p==NULL||q==NULL) return root;
   TreeNode* visiting = root;
   while(visiting!=NULL){
      if (visiting->val>p->val&&visiting->val>q->val)
      {
         visiting = visiting->left; 
      }else if(visiting->val<p->val&&visiting->val<q->val){
          visiting = visiting->right;
      }else{
          return visiting;
      }
   }
   return visiting;
 }
```
#### [转双向链表](https://www.nowcoder.com/practice/947f6eb80d944a84850b0538bf0ec3a5?tpId=13&tqId=11179&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```
TreeNode* Convert(TreeNode* pRootOfTree)
{
   if (pRootOfTree==NULL) return pRootOfTree;
   stack<TreeNode*> visited;
   TreeNode* visiting = pRootOfTree;
   TreeNode* last = NULL;
   TreeNode* head = NULL;
   while(visiting!=NULL||!visited.empty())
   {
      if (visiting!=NULL)
      {
          visited.push(visiting);
          visiting = visiting->left;
      }else{
          visiting = visited.top();
          if(last!=NULL)
          {
              last->right=visiting;
              visiting->left=last;
              last = visiting;

          }else{
              last = visiting;
              head = visiting;
          }
          visited.pop();
          visiting = visiting->right;
      }  
   }
   return head;
}
```
#### 深度
##### 求最大深度
```
int TreeDepth(TreeNode* pRoot)
{
  if (pRoot == NULL) return 0;
  return max(1+TreeDepth(pRoot->left),1+TreeDepth(pRoot->right));
}
```
#### 根据遍历结果反推
##### [重建二叉树](https://www.nowcoder.com/practice/8a19cbe657394eeaac2f6ea9b0f6fcf6?tpId=13&tqId=11157&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```
TreeNode* reConstruct(vector<int> pre,vector<int> in,int ps,int pe,int is,int ie) {
   //pre {1,2,4,7,3,5,6,8}
   //in {4,7,2,1,5,3,8,6}
   if (ps>pe||is>ie)
   {
      return NULL;
   }
   struct TreeNode* root = new TreeNode(pre[ps]);
   if (ps==pe||is==ie)
   {
      root->right = NULL;
      root->left = NULL;
   }else{
      int i = is; //找到对应节点，递归
      for (; i <= ie; ++i)
      {
         if (in[i]==root->val)
         {
            break;
         }
      }
      root->left = reConstruct(pre,in,ps+1,ps+i-is,is,i-1);
      root->right = reConstruct(pre,in,ps+i-is+1,pe,i+1,ie);
   }
   return root;
 }

TreeNode* reConstructBinaryTree(vector<int> pre,vector<int> in) {
   if (pre.empty()||in.empty())
   {
      return NULL;
   }
   struct TreeNode* root;
   root = reConstruct(pre,in,0,pre.size()-1,0,in.size()-1);
   return root;
 }
```
