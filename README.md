# BJIT Trainee 
**Task #1**
## Rotate Array
> Sample Input Output
```
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```
> Approach
```
reverse last k numbers first, then 0th to k-1 numbers should be reversed.
then fully reverse the array.
```
> Example

```
1-2-3-4-5-6-7
k=3
(1-2-3-4)-(5-6-7)
(4-3-2-1)-(7-6-5)
5-6-7-1-2-3-4
```


> My Code
```
class Solution {
public:
    void reverse(vector<int>& num, int low, int high)
    {
        while(low<high)
        {
            swap(num[low],num[high]);
            low++;
            high--;
        }   
    }
    void rotate(vector<int>& nums, int k) {
        int n=nums.size();
        k=k%n;
        reverse(nums,0,n-k-1);
        reverse(nums,n-k,n-1);
        reverse(nums,0,n-1);
        
    }
};
```
**Task #2*
## Move Zeroes
Given an integer array nums, move all 0's to the end of it 
while maintaining the relative order of the non-zero elements.
Note that you must do this in-place without making a copy of the array.

> Sample Input Output
```
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
Input: nums = [0]
Output: [0]
```
> Approach
```
if non zero found, swap with nums[j], which starts from 0, and j++.
```
> My Code
```
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        for (int i=0,j=0; i<nums.size(); i++)
        {
            if(nums[i])
            {
               swap(nums[i],nums[j]);
               j++;
            }
        }
    }
};
```
**Task #3**
## Contains Duplicate
> Sample Input Output
```
Input: nums = [1,2,3,1]
Output: true
Input: nums = [1,2,3,4]
Output: false
```
> Approach
```
copy the vector into map, map means no repect.
so,both vector and map same size means no duplicate.
```
> My Code
```
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        int s=nums.size();
        map <int,int> m;
        for(int i=0; i<s;i++)
        {
            m[nums[i]]++;
        }
        if(m.size()==s)
            return false;
        else
            return true;
    }
};
```


**Task #1**
## 
> Sample Input Output
```

```
>Approach
```

```
> My Code
```

```
>Best Code
```

```
