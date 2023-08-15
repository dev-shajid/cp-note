# Basic Problem with Array

>- [LeetCode Article - Sliding Window](https://leetcode.com/discuss/study-guide/3722472sliding-window-technique-a-comprehensive-guide)
>- [LeetCode Article - 25 variation of two sum](https://leetcode.com/discuss/interview-question/3685049/25-variations-of-two-sum-question)

### Problem
- [1. Remove Duplicate](#p1)
- [2. Rotate an Array to left by 'd' steps](#p2)
- [3. Move all zero to the end of Array](#p3)
- [4. Union of 2 sorted Array](#p4)
- [5. Intersection of 2 sorted Array](#p5)
- [6. Find missing number](#p6)
- [7. Two Sum](#p7)


<p id='p1'/>

## 1. Remove Duplicate 
* [Problem 
    <img align="center" height="15" src="https://leetcode.com/_next/static/images/logo-dark-c96c407d175e36c81e236fcfdd682a0b.png">
](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)


 **Brute Force Solution**
 ```c++
    int arr[]={1,1,1,2,2,2,2,3,3,3,4};
    int n=sizeof(arr)/sizeof(arr[0]);
    
    set<int> s;
    for(auto v:arr) s.insert(v);

    for(auto v:s) cout << v << " ";
    cout << endl << "Size: " << s.size() << endl;
 ```
> * **Time Complexity:** O(nlogn)
> * **Space Complexity:** O(4)

***
 **Optimal Solution** (*Tow Pointer Method*)
 ```c++
    int arr[]={1,1,1,2,2,2,2,3,3,3,4};
    int n=sizeof(arr)/sizeof(arr[0]);
    
    int i=1;
    for(int j=1; j<n; j++){
        if(arr[j]!=arr2[i-1]){
        arr[i++]=arr[j];
        }
    }

    for(int j=0; j<i; j++) cout << arr[j] << " ";
    cout << endl << "Size: " << i << endl;
 ```
> * **Time Complexity:** O(n)
> * **Space Complexity:** O(1)
***


<p id='p2'/>

## 2. Rotate an Array to left by 'd' steps
* [Problem 
    <img align="center" height="15" src="https://leetcode.com/_next/static/images/logo-dark-c96c407d175e36c81e236fcfdd682a0b.png">
](https://leetcode.com/problems/rotate-array/)

 **Solution: 1**
 ```c++
    int n=7, d=3;
    // rotating array n times remains the array unchanged
    d=d%n; // if d=10-->d=d%n=3
    int arr[]={1,2,3,4,5,6,7}, tmp[d];
    
    // Store first d element in tmp array
    for(int i=0; i<d; i++) tmp[i]=arr[i];
    // Shifting all elements after first d elements to 1st portion
    for(int i=d; i<n; i++) arr[i-d]=arr[i];
    /* Now assigning stored 1st d element in tmp
     array to last portion of the actual array */
    for(int i=n-d; i<n; i++) arr[i]=tmp[i-(n-d)];

    // Output
    for(auto i:arr) cout << i << " "; // 4 5 6 7 1 2 3
 ```
> * **Time Complexity:** O(n+d)
> * **Space Complexity:** O(d)

***

 **Solution: 2**

 ```c++
    void reverse(int arr[], int l, int r){
        for(int i=l; i<(l+r)/2; i++) swap(arr[i],arr[r+l-i-1]);
    }
 ```
 ```c++
    int n=7, d=3;
    // rotating array n times remains the array unchanged
    d=d%n; // if d=10-->d=d%n=3
    int arr[]={1,2,3,4,5,6,7};

    // Reverse 1st d elements
    reverse(arr,0,d);
    // Reverse last (n-d) elements
    reverse(arr,d,n);
    // Now reverse whole array
    reverse(arr,0,n);

    // Output
    for(auto i:arr) cout << i << " "; // 4 5 6 7 1 2 3
 ```
> * **Time Complexity:** O(2n)
> * **Space Complexity:** O(1)
***


<p id='p3'/>

## 3. Move all zero to the end of Array
* [Problem 
    <img align="center" height="15" src="https://leetcode.com/_next/static/images/logo-dark-c96c407d175e36c81e236fcfdd682a0b.png">
](https://leetcode.com/problems/move-zeroes/)

 <!-- **Solution: 1** -->
 ```c++
    int n=11;
    int arr[]={1,0,0,2,3,0,0,0,4,0,5};
    int l=0;
    for(int r=0; r<n; r++){
        if(arr[r]) arr[l++]=arr[r];
        if(r!=l-1) arr[r]=0;
    }
 ```
> * **Time Complexity:** O(n)
> * **Space Complexity:** O(1)

***


<p id='p4'/>

## 4. Union of 2 sorted Array
* [Problem 
    <img align="center" height="15" src="https://leetcode.com/_next/static/images/logo-dark-c96c407d175e36c81e236fcfdd682a0b.png">
](https://leetcode.com/problems/two-sum/)

**If there is no duplicate element**

 ```c++
    int n=6, m=4;
    int arr1[]={1,3,6,8,9,10}, arr2[]={2,5,12,14};
    int arr[m+n];
    int i=0, j=0, k=0;

    while(i<n && j<m){
        if(arr1[i]<arr2[j]){
        arr[k++] = arr1[i++];
        }else{
        arr[k++] = arr2[j++];
        }
    }

    while(i<n) arr[k++] = arr1[i++];

    while(j<m) arr[k++] = arr2[j++];

    // Output
    for(auto x : arr )cout<<x<<" ";
    // 1 2 3 5 6 8 9 10 12 14
 ```
> * **Time Complexity:** O(n+m)
> * **Space Complexity:** O(1)

***

 **If there are Duplicate elements**
 ```c++
    int n=9, m=6;
    int arr1[]={1,1,3,3,6,8,9,9,10}, arr2[]={2,5,5,12,14,14};
    int arr[m+n];
    int i=0, j=0, k=0;

    while(i<n && j<m){
        if(arr1[i]<arr2[j]){
            if(!k || arr[k-1]!=arr1[i]) arr[k++] = arr1[i];
            i++;
        }else{
            if(!k || arr[k-1]!=arr2[j]) arr[k++] = arr2[j];
            j++;
        }
    }

    while(i<n){
        if(!k || arr[k-1]!=arr1[i]) arr[k++] = arr1[i];
        i++;
    }

    while(j<m){
        if(!k || arr[k-1]!=arr2[j]) arr[k++] = arr2[j];
        j++; 
    }

    // Output
    for(int x=0; x<k; x++)cout<<arr[x]<<" ";
    // 1 2 3 5 6 8 9 10 12 14
 ```
> * **Time Complexity:** O(n+m)
> * **Space Complexity:** O(1)

***


<p id='p5'/>

## 5. Intersection of 2 sorted Array
* [Problem 
    <img align="center" height="15" src="https://leetcode.com/_next/static/images/logo-dark-c96c407d175e36c81e236fcfdd682a0b.png">
](https://leetcode.com/problems/intersection-of-two-arrays/)

 <!-- **If there are Duplicate elements** -->
 ```c++
    int n=7, m=6;
    int arr1[]={1,2,3,4,6,8,10}, arr2[]={2,3,3,5,6,14};
    int arr[m+n];
    int i=0, j=0, k=0;

    while(i<n && j<m){
        if(arr1[i]>arr2[j]) j++;
        else if(arr1[i]<arr2[j]) i++;
        else {
            arr[k]=arr1[i];
            i++, j++, k++;
        }
    }

    // Output
    for(int x=0; x<k; x++)cout<<arr[x]<<" ";
    // 2 3 6
 ```
> * **Time Complexity:** O(n+m)
> * **Space Complexity:** O(1)

***


<p id='p6'/>

## 6. Find missing number

* [Problem 
    <img align="center" height="15" src="https://leetcode.com/_next/static/images/logo-dark-c96c407d175e36c81e236fcfdd682a0b.png">
](https://leetcode.com/problems/missing-number/)


 **Summation Method**
 ```c++
    int n=5;
    int a[] ={1,2,4,5};
    int sum=(n*(n+1))/2;
    for(int i=0; i<n; i++) sum-=arr[i];
    cout << sum << endl;
    // 3 is the missing number here
 ```
> * **Time Complexity:** O(n)
> * **Space Complexity:** O(1)
---
 **Using XOR operator**
 ```c++
    int n=5;
    int a[] ={1,2,4,5};
    int xOr=0;
    for(int i=0; i<n-1; i++) xOr^=arr[i]^(i+1);
    xOr^=n;
    cout << xOr << endl;
    // 3 is the missing number here
 ```
> * **Time Complexity:** O(n)
> * **Space Complexity:** O(1)

>***Here summation may be overflow for large integer, xor method is more optimal solution than the first one***

***

<p id='p7'/>

## 7. Two Sum
* [Problem 
    <img align="center" height="15" src="https://leetcode.com/_next/static/images/logo-dark-c96c407d175e36c81e236fcfdd682a0b.png">
](https://leetcode.com/problems/two-sum/)

 **Brute Force**
 ```c++
    vector<int> twoSum(vector<int>& nums, int k) {
        for(int i=0; i<nums.size()-1; i++){
            for(int j=i+1; j<nums.size(); j++){
                if(nums[i]+nums[j]==k) return {i,j};
            }
        }
        return 0;
    }
 ```
> * **Time Complexity:** O(n^2)
> * **Space Complexity:** O(2)

<!-- >****** -->
---
 **Optimal Solution(Hashmap)**
 ```c++
    vector<int> twoSum(vector<int>& nums, int k) {
        unordered_map<int,int> m;
        for(int i=0; i<nums.size(); i++){
            int c=k-nums[i];
            if(m.count(c)) return {m[c], i};
            m[nums[i]]=i;
        }
        return {};
    }
 ```
> * ***Time Complexity:*** O(n^2) or O(nlogn)
> * ***Space Complexity:*** O(1)

***map o(nlogn)</br>unordered_map o(n^2)***

---
 **Optimal Solution(2 Pointer)**
 ```c++
    vector<int> twoSum(vector<int>& nums, int k) {
        sort(nums.begin(),nums.end());
        int n=nums.size(), l=0, r=n-1;
        while (l<r){
            long sum =  nums[l] + nums[r];
            if(sum == k ) break;
            else if(sum > k ) --r; //move right pointer to left
            else ++l; //if sum is less than K then move the left pointer to right
        }

        return {l,r};
    }
 ```
> * **Time Complexity:** O(n) + O(nlogn)
> * **Space Complexity:** O(1)

***For sorting o(nlogn) & for while loop o(n)***

***