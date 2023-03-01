# BJIT Trainee 
**task #0**

# Counting Sort

# Complexity
- Time complexity: ***O(n+k)***
<!-- Add your time complexity here, e.g. $$O(n)$$ -->

- Space complexity:***O(n)***
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

# Code
```
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
    countingSort(nums);
    return nums;
    }
 void countingSort(vector<int>& nums)
 {
    unordered_map<int,int> counts;

    int mini=*min_element(nums.begin(),nums.end());
    int maxi=*max_element(nums.begin(),nums.end());

    for(auto & val: nums) counts[val]++;

    int index=0;
    for(int i=mini; i<=maxi; i++)
    {
        while(counts[i]>0)
        {
            nums[index]=i;
            index++;
            counts[i]--;
        }
    }
 }
};
```
# Merge Sort

# Complexity
- Time complexity:  ***O(nlogn)***
<!-- Add your time complexity here, e.g. $$O(n)$$ -->

- Space complexity:  ***O(n)***
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

# Code
```
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
    mergeSort(nums,0,nums.size()-1);
    return nums;
    }
void merge(vector<int>&nums,int start, int mid, int end)
{
    int p=start;
    int q=mid+1;
    vector<int>num(end-start+1,-1);
    int k=0;

    for(int i=start; i<=end; i++)
    {
        if(p>mid) num[k++]=nums[q++];
        else if(q>end) num[k++]=nums[p++];
        else if(nums[p]>nums[q]) num[k++]=nums[q++];
        else
        num[k++]=nums[p++];
    }
    for(int i=0; i<k; i++)
     nums[start++]=num[i];
}
void mergeSort(vector<int>&nums,int start, int end)
{
    if(start<end) 
    {
        int mid=(start+end)/2;
        mergeSort(nums,start,mid);
        mergeSort(nums,mid+1,end);
        merge(nums,start,mid,end);
    }
}
};
```
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
**Task #2**
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


**Task #4**
## Linked List
Write a function to remove duplicate item in a linked link L
where the head is given and return the list L

> Sample Input Output
```Original list: 1 2 3 2 4 
List after removing duplicates: 1 2 3 4 
```
>Approach
```
This code defines the Node struct, the removeDuplicates function that was explained earlier, 
and a printList function that prints the values of a linked list. The main function creates 
a sample linked list with duplicate values, prints the original list, 
calls the removeDuplicates function, prints the modified list, and 
then returns 0 to indicate successful execution.
```
> My Code
```
#include <iostream>
#include <unordered_set>

struct Node {
    int val;
    Node* next;
    Node(int x) : val(x), next(nullptr) {}
};

Node* removeDuplicates(Node* head) {
    std::unordered_set<int> seen;
    Node* curr = head;
    Node* prev = nullptr;

    while (curr) {
        if (seen.count(curr->val)) {
            prev->next = curr->next;
            delete curr;
            curr = prev->next;
        } else {
            seen.insert(curr->val);
            prev = curr;
            curr = curr->next;
        }
    }

    return head;
}

void printList(Node* head) {
    Node* curr = head;
    while (curr) {
        std::cout << curr->val << " ";
        curr = curr->next;
    }
    std::cout << std::endl;
}

int main() {
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(2);
    head->next->next->next->next = new Node(4);

    std::cout << "Original list: ";
    printList(head);

    head = removeDuplicates(head);

    std::cout << "List after removing duplicates: ";
    printList(head);

    return 0;
}

```
**Task #5**
## Recursion Function
Write a recursive function to output the digit in Number N.
> Sample Input Output
```
input: 123
output: 1 2 3
```
> My Code
```
#include <iostream>

void outputDigits(int n) {
    if (n < 10) {
        std::cout << n << " ";
        return;
    }
    outputDigits(n / 10);
    std::cout << n % 10 << " ";
}

int main() {
    int n = 123456;
    std::cout << "Digits in " << n << " are: ";
    outputDigits(n);
    std::cout << std::endl;
    return 0;
}
```

**task #6**
## Abbreviation
write a function to check abbreviation is correct or Not.
> Sample Input Output
```
String A: Bangladesh Japan Information Technology
String B: BJIT
output: true
```

**task #7**
## Palindrome Check
write a function to check palindrome Using both STACK and QUEUE.

**task #8**
## Consecutive Triplet
Find total number of Consecutive triplet in a given array.
> Sample Input Output
```
input: 3 2 4 5 6 8 9 10 (not sorted)
output: 3 
explanation: ( 2 3 4), (3,4,5), (8,9,10)
```
**task #9**
## ADDITION & SUBTRACTION
How do you perform addition and substraction of two huge numbers (bigger than INT_MAX).
> Sample Input Output
```
input:
output:
```
**task #10**
## Duplicate Words
A string contains words, count how many duplictae words are there.
> Sample Input Output
```
input: i am a boy, i can cook.
output:1 (i)
```
**task #11**
## Kadane's Algorithm

**task #12**
## Min heap Implementation

**task #13**
## Number theory
A integer N is given, find x and y where x*y==n and abs(x-y) is minimum of all possible x,y.

**task #14**
## Redundant Words
1.Find redundant words in a given string.
2. Size of arrays after removing duplicate.

**task #15**
## Sub string
Find longest non-repeatable sub-string.



