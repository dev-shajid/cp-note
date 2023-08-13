# Problem with Array (Medium)

- [1. Maximum subarray sum](#p1)
- [2. Longest Subarray with given Sum K](#p2)
- [3. Rearrange Array Elements by Sign](#p3)





<p id='p1'/>

## 1. Maximum subarray sum
* [Problem](https://www.codingninjas.com/studio/problems/maximum-subarray-sum_630526)

 **Brute Force**
 ```c++
    int n=8;
    int arr[]={1,-2,4,3,-2,1,-4,6};
    int mx=0;
    
    for(int i=0; i<n; i++){
        int s=0;
        for(int j=i; j<n; j++) s+=arr[j], mx=max(mx,s);
    }
    cout << mx << endl;
 ```
> * **Time Complexity:** O(n^2)
> * **Space Complexity:** O(1)

>***Here we are calculating sum for every possible subarray and taking the maximum one***
---
 **Optimal Solution:**
 ```c++
    int n=8;
    int arr[]={1,-2,4,3,-2,1,-4,6};
    int mx=0, s=0;
    
    for(int i=0; i<n; i++){
        int s+=arr[i];
        mx=max(mx,s);
        if(s<0) s=0;
    }
    cout << mx << endl;
 ```
> * **Time Complexity:** O(n)
> * **Space Complexity:** O(1)

>***If the sum is less than 0, making it 0. Because, there is no contributinon in max sum by negative summation.***

***




<p id='p2'/>

## 2. Longest Subarray with given Sum K
- [Problem(Positive)](https://www.codingninjas.com/studio/problems/longest-subarray-with-sum-k_6682399)
- [Problem(Negative)](https://www.codingninjas.com/studio/problems/longest-subarray-with-sum-k_5713505)

 **Brute Force**
 ```c++
    int n=7, k=3;
    int arr[]={1,2,3,1,1,1,1};
    int len=0;
    
    for(int i=0; i<n; i++){
        int s=0;
        for(int j=i; j<n; j++) {
            s+=arr[j];
            if (s == k) len = max(len, j - i + 1);
        }
    }
    cout << len << endl; // 3
 ```
> * **Time Complexity:** O(n^2)
> * **Space Complexity:** O(1)

>***Here we are calculating sum of every subarray can be formmed form the given array.***
---
 **Better Approach(Using Hashing):**
 ```c++
    int n=7, k=7;
    int arr[]={3,4,3,-3,2,1,-3};
    map<int,int> m;
    int ans=0, sum=0;
    for(int i=0; i<n; i++){
        sum+=arr[i];
        if(sum==k) ans=i+1;
        else if(m.count(sum-k)) ans=max(ans,i-m[sum-k]);
        else if(!m.count(sum)) m[sum]=i;
    }
    cout << ans << endl; // 7
 ```
> * **Time Complexity:** O(nlogn)
> * **Space Complexity:** O(n)

>![Alt](https://takeuforward.org/wp-content/uploads/2023/04/Screenshot-2023-04-13-004939.png)
>![Alt](https://takeuforward.org/wp-content/uploads/2023/04/Screenshot-2023-04-13-005443.png)
---
 **Optimal Solution(2 Pointer)**
 ```c++
    int longestSubarrayWithSumK(vector<int> nums, long long k) {
        int n=nums.size(), l=0, r=0, ans=0;
        long long sum=0;
        while(r<n){
            sum+=nums[r++];
            while(l<r && sum>k){
                sum-=nums[l];
                l++;
            }
            if(sum==k) ans=max(ans, r-l);
        }
        return ans;
    }
 ```
> * **Time Complexity:** O(2n)
> * **Space Complexity:** O(1)

>***This code will not work for the array consisting negative elements***

***



<p id='p3'/>

## 3. Rearrange Array Elements by Sign
- [Problem-codingninjas](https://www.codingninjas.com/studio/problems/alternate-numbers_6783445)
- [Problem-leetcode](https://leetcode.com/problems/rearrange-array-elements-by-sign)

 **Brute Force**
 ```c++
    vector<int> rearrangeArray(vector<int>& v) {
        int n=v.size(), p=0, n=0;
        vector<int> p_e, n_e;
        for(auto i:v){
            if(i<0) n_e.push_back(i);
            else p_e.push_back(i);
        }

        for(int i=0; i<m/2; i++){
            v[2*i]=p_e[i];
            v[2*i+1]=n_e[i];
        }

        return v;
    }
 ```
> * **Time Complexity:** O(n)+O(n)
> * **Space Complexity:** O(n)
---

 **Optimal-1**
 ```c++
    vector<int> rearrangeArray(vector<int>& v) {
        int m=v.size(), p=0, n=1;
        vector<int> ans(m);
        for(auto i:v){
            if(i>=0) ans[p]=i, p+=2;
            else ans[n]=i, n+=2;
        }
        return ans;
    }
 ```
> * **Time Complexity:** O(n)
> * **Space Complexity:** O(n)
---

 **Optimal-2**
 ```c++
    vector<int> rearrangeArray(vector<int>& v) {
        vector<int> ans;
        int m=v.size(), p=0, n=0;
        while(p<m && n<m){
            if(v[p]<0) p++; // find the index of next positive element
            if(v[n]>0) n++; // find the index of next negative element
            // Push both pos & neg element in ans when they are found and increase their index
            if(v[p]>0 && v[n]<0) ans.push_back(v[p++]), ans.push_back(v[n++]);
            
        }

        return ans;
    }
 ```
> * **Time Complexity:** O(n)
> * **Space Complexity:** O(n)

***

