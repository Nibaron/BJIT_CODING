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
> Code
```
#include<bits/stdc++.h>
using namespace std;

bool validWordAbbreviation(string word, string abbr) {
    string abr="";
    abr+=word[0];
    for(int i=1; i<word.size(); i++)
    {
        if(word[i]==' ') 
         abr+=word[i+1];
    }
    return abbr==abr;
}

int main() {
    string word = "Bangladesh Japan Information Technology";
    string abbr = "BJIT";
    if (validWordAbbreviation(word, abbr))
    cout << abbr << " is a valid abbreviation of " << word << std::endl;
    else 
    cout << abbr << " is not a valid abbreviation of " << word << std::endl;
    return 0;
}
```
**task #7**
## Palindrome Check
write a function to check palindrome Using both STACK and QUEUE.

> STACK
```
#include <iostream>
#include <stack>
#include <string>

using namespace std;

bool isPalindrome(string str) {
    stack<char> stk;

    // push all characters onto the stack
    for (int i = 0; i < str.length(); i++) {
        char c = tolower(str[i]);
        if (isalpha(c)) {
            stk.push(c);
        }
    }

    // pop from stack and compare to original string
    for (int i = 0; i < str.length(); i++) {
        char c = tolower(str[i]);
        if (isalpha(c) && c != stk.top()) {
            return false;
        }
        if (isalpha(c)) {
            stk.pop();
        }
    }

    return true;
}

int main() {
    string str;
    cout << "Enter a string: ";
    getline(cin, str);

    if (isPalindrome(str)) {
        cout << str << " is a palindrome." << endl;
    } else {
        cout << str << " is not a palindrome." << endl;
    }

    return 0;
}
```
> QUEUE
```
#include <iostream>
#include <queue>
#include <string>

using namespace std;

bool isPalindrome(string str) {
    queue<char> que;

    // push all characters onto the queue
    for (int i = 0; i < str.length(); i++) {
        char c = tolower(str[i]);
        if (isalpha(c)) {
            que.push(c);
        }
    }

    // dequeue from queue and compare to original string
    for (int i = str.length()-1; i >=0; i--) {
        char c = tolower(str[i]);
        if (isalpha(c) && c != que.front()) {
            return false;
        }
        if (isalpha(c)) {
            que.pop();
        }
    }

    return true;
}

int main() {
    string str;
    cout << "Enter a string: ";
    getline(cin, str);

    if (isPalindrome(str)) {
        cout << str << " is a palindrome." << endl;
    } else {
        cout << str << " is not a palindrome." << endl;
    }

    return 0;
}

```

**task #8**
## Consecutive Triplet
Find total number of Consecutive triplet in a given array.
> Sample Input Output
```
input: 3 2 4 5 6 8 9 10 (not sorted)
output: 3 
explanation: ( 2 3 4), (3,4,5), (8,9,10)
```
> Code
```
#include <iostream>
using namespace std;

int countConsecutiveTriplets(int arr[], int n) {
    int count = 0;

    for (int i = 0; i < n - 2; i++) {
        if (arr[i] + 1 == arr[i+1] && arr[i+1] + 1 == arr[i+2]) {
            count++;
        }
    }

    return count;
}

int main() {
    int arr[] = {1, 2, 3, 5, 6, 7, 8, 10, 12, 13};
    int n = sizeof(arr) / sizeof(arr[0]);

    int totalCount = countConsecutiveTriplets(arr, n);

    cout << "Total number of consecutive triplets: " << totalCount << endl;

    return 0;
}

```
**task #9**
## ADDITION & SUBTRACTION
How do you perform addition and substraction of two huge numbers (bigger than INT_MAX).
> Sample Input Output
```
input:
output:
```
> code
```
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

string add(string a, string b) {
    string res;
    int carry = 0, i = a.length() - 1, j = b.length() - 1;

    while (i >= 0 || j >= 0 || carry) {
        int sum = carry;
        if (i >= 0) sum += a[i--] - '0';
        if (j >= 0) sum += b[j--] - '0';
        carry = sum / 10;
        res.push_back((sum % 10) + '0');
    }

    reverse(res.begin(), res.end());
    return res;
}

string subtract(string a, string b) {
    string res;
    int borrow = 0, i = a.length() - 1, j = b.length() - 1;

    while (i >= 0 || j >= 0) {
        int diff = borrow;
        if (i >= 0) diff += a[i--] - '0';
        if (j >= 0) diff -= b[j--] - '0';
        borrow = (diff < 0);
        res.push_back((borrow ? diff + 10 : diff) + '0');
    }

    reverse(res.begin(), res.end());
    return res;
}

int main() {
    string a = "12345678901234567890";
    string b = "98765432109876543210";

    cout << "a + b = " << add(a, b) << endl;
    cout << "a - b = " << subtract(a, b) << endl;

    return 0;
}

```
**task #10**
## Duplicate Words
A string contains words, count how many duplictae words are there.
> Sample Input Output
```
input: i am a boy, i can cook.
output: i : 2
```
> code
```
#include <iostream>
#include <string>
#include <sstream>
#include <unordered_map>

int main() {
    std::string sentence = "The quick brown fox jumps over the lazy dog. The dog jumps over the fence.";
    std::stringstream ss(sentence);
    std::unordered_map<std::string, int> wordCount;

    // loop through each word in the sentence
    std::string word;
    while (ss >> word) {
        // increment the count for this word in the map
        wordCount[word]++;
    }

    // output the results
    std::cout << "Duplicate words in the sentence: " << std::endl;
    for (auto& pair : wordCount) {
        if (pair.second > 1) {
            std::cout << pair.first << " : " << pair.second << std::endl;
        }
    }

    return 0;
}

```

**task #11**
## Min heap Implementation
> code
```
#include <iostream>
#include <vector>

class MinHeap {
private:
    std::vector<int> heap;

    void heapifyUp(int index) {
        if (index == 0) {
            return;
        }
        int parentIndex = (index - 1) / 2;
        if (heap[index] < heap[parentIndex]) {
            std::swap(heap[index], heap[parentIndex]);
            heapifyUp(parentIndex);
        }
    }

    void heapifyDown(int index) {
        int leftChildIndex = 2 * index + 1;
        int rightChildIndex = 2 * index + 2;
        int smallestIndex = index;
        if (leftChildIndex < heap.size() && heap[leftChildIndex] < heap[smallestIndex]) {
            smallestIndex = leftChildIndex;
        }
        if (rightChildIndex < heap.size() && heap[rightChildIndex] < heap[smallestIndex]) {
            smallestIndex = rightChildIndex;
        }
        if (smallestIndex != index) {
            std::swap(heap[index], heap[smallestIndex]);
            heapifyDown(smallestIndex);
        }
    }

public:
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    int pop() {
        if (heap.empty()) {
            throw std::out_of_range("Heap is empty");
        }
        int value = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
        return value;
    }

    int size() {
        return heap.size();
    }

    bool empty() {
        return heap.empty();
    }
};

int main() {
    MinHeap minHeap;
    minHeap.insert(10);
    minHeap.insert(5);
    minHeap.insert(7);
    minHeap.insert(3);
    minHeap.insert(1);

    std::cout << "Min heap size: " << minHeap.size() << std::endl;

    while (!minHeap.empty()) {
        std::cout << minHeap.pop() << " ";
    }
    std::cout << std::endl;

    return 0;
}

```
**task #12**
## Number theory
A integer N is given, find x and y where x*y==n and abs(x-y) is minimum of all possible x,y.

> Sample Input and Output
```
imput:12
output: 3 4
```
>code
```
#include <bits/stdc++.h>
using namespace std;

void printPFsInPairs(int n)
{
    int mul1=1,mul2=n;
    for (int i = 1; i * i <= n; i++)
    {
        if (n % i == 0)
        {
            int a=i;
            int b=n/i;
            if(mul2-mul1 > b-a)
            {mul1=a;mul2=b;}
        }
    }
    cout<<mul1<<" "<<mul2;
}
 
// Driver code
int main()
{
    int n = 12;
    printPFsInPairs(n);
    return 0;
}

```
**task #13**
## Sub string
Find longest non-repeatable sub-string.

>Code
```
#include <iostream>
#include <unordered_map>
#include <string>

using namespace std;

string longestNonRepeatingSubstring(string str) {
    unordered_map<char, int> charMap;
    int start = 0, maxLength = 0;
    for (int i = 0; i < str.length(); i++) {
        char c = str[i];
        if (charMap.find(c) != charMap.end() && charMap[c] >= start) {
            // If the current character has already appeared in the current substring,
            // update the starting index of the current substring to the position after
            // the last occurrence of the character.
            start = charMap[c] + 1;
        }
        charMap[c] = i; // Update the last occurrence of the character
        int length = i - start + 1; // Calculate the length of the current substring
        if (length > maxLength) {
            maxLength = length;
        }
    }
    return str.substr(start, maxLength);
}

int main() {
    string str = "pwwkew";
    string longestSubstr = longestNonRepeatingSubstring(str);
    cout << "The longest non-repeating substring in \"" << str << "\" is \"" << longestSubstr << "\"." << endl;
    return 0;
}
```

