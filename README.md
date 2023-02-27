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

reverse last k numbers first, then 0th to k-1 numbers should be reversed.
then fully reverse the array.

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
**Task #2**
## Contains Duplicate
> Sample Input Output
```
Input: nums = [1,2,3,1]
Output: true
Input: nums = [1,2,3,4]
Output: false
```
> Approach

copy the vector into map, map means no repect.
so,both vector and map same size means no duplicate.


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
> My Code
```

```
>Best Code
```

```
