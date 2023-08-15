# Problem with Array (Medium)

- [1. Maximum subarray sum (Kaden's Algorithm)](#p1)
- [2. Count all Subarray Sum Equals K](#p2)
- [3. Longest Subarray Sum Equals K](#p3)
- [4. Rearrange Array Elements by Sign](#p4)
- [5. Majority Elements (for n/2)](#p5)
- [6. Majority Elements 2 (for n/3)](#p6)
- [7. Three Sum](#p7)
- [8. Set Matrix Zeroes](#p8)
- [9. Spiral Traversal of Matrix](#p9)





<p id='p1'/>

## 1. Maximum subarray sum (Kaden's Algorithm)
* [Problem 
    <img align="center" height="15" src="https://leetcode.com/_next/static/images/logo-dark-c96c407d175e36c81e236fcfdd682a0b.png">
](https://leetcode.com/problems/maximum-subarray/)
* [Problem 
    <img align="center" height="15" src="https://takeuforward.org/wp-content/uploads/2023/04/Group-11-5.png">
](https://www.codingninjas.com/studio/problems/maximum-subarray-sum_630526)

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

## 2. Count all Subarray Sum Equals K

- [Problem 
    <img align="center" height="15" src="https://leetcode.com/_next/static/images/logo-dark-c96c407d175e36c81e236fcfdd682a0b.png">
](https://leetcode.com/problems/subarray-sum-equals-k/)
- [Problem 
    <img align="center" height="15" src="https://takeuforward.org/wp-content/uploads/2023/04/Group-11-5.png">
](https://www.codingninjas.com/studio/problems/subarray-sums-i_1467103/)

 **Brute Force**
 ```c++
    int n=7, k=3;
    int arr[]={1,2,3,1,1,1,1};
    int ans=0;
    
    for(int i=0; i<n; i++){
        int s=0;
        for(int j=i; j<n; j++) {
            s+=arr[j];
            if (s == k) ans++;
        }
    }
    cout << ans << endl; // 3
 ```
> * **Time Complexity:** O(n^2)
> * **Space Complexity:** O(1)

>***Here we are calculating sum of every subarray can be formmed form the given array.***
---
 **Optimal Solution(Using Hashing):**
 ```c++
    int subarraySum(vector<int>& nums, int k) {
        int n=nums.size(), sum=0, ans=0;
        unordered_map<int,int> m;
        m[0]=1;
        for(int i=0; i<n; i++){
            sum+=nums[i];
            if(m.count(sum-k)) ans+=m[sum-k];
            m[sum]++;
        }
        return ans;
    }
 ```
> * **Time Complexity:** O(nlogn)
> * **Space Complexity:** O(n)

>![Alt](https://takeuforward.org/wp-content/uploads/2023/04/Screenshot-2023-04-13-004939.png)
>![Alt](https://takeuforward.org/wp-content/uploads/2023/04/Screenshot-2023-04-13-005443.png)

***



<p id='p3'/>

## 3. Longest Subarray with given Sum K
- [Problem(Positive) 
    <img align="center" height="15" src="https://takeuforward.org/wp-content/uploads/2023/04/Group-11-5.png">
](https://www.codingninjas.com/studio/problems/longest-subarray-with-sum-k_6682399)
- [Problem(Negative) 
    <img align="center" height="15" src="https://takeuforward.org/wp-content/uploads/2023/04/Group-11-5.png">
](https://www.codingninjas.com/studio/problems/longest-subarray-with-sum-k_5713505)

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
 **Optimal Solution(Using Hashing):**
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



<p id='p4'/>

## 4. Rearrange Array Elements by Sign
- [Problem 
    <img align="center" height="15" src="https://takeuforward.org/wp-content/uploads/2023/04/Group-11-5.png">
](https://www.codingninjas.com/studio/problems/alternate-numbers_6783445)
- [Problem 
    <img align="center" height="15" src="https://leetcode.com/_next/static/images/logo-dark-c96c407d175e36c81e236fcfdd682a0b.png">
](https://leetcode.com/problems/rearrange-array-elements-by-sign)

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


<p id='p5'/>

## 5. Majority Elements (for n/2)
- [Problem
<img align="center" height="15" src="https://leetcode.com/_next/static/images/logo-dark-c96c407d175e36c81e236fcfdd682a0b.png">
](https://leetcode.com/problems/majority-element/)
- [Problem 
    <img align="center" height="15" src="https://takeuforward.org/wp-content/uploads/2023/04/Group-11-5.png">
](https://www.codingninjas.com/studio/problems/majority-element_6915220)

 **Better Approach**
 ```c++
    int majority(vector<int>& v) {
        int n=v.size();
        map<int,int> m;
        for(auto i:v) m[i]++;

        for(auto [k,v]:m){
            if(v>n/2) return k;
        }

        return -1;
    }
 ```
> * **Time Complexity:** O(n.logn)
> * **Space Complexity:** O(n)
---

 **Optimal**
 ```c++
    int majority(vector<int>& v) {
        int n=v.size(), cnt=0, ele=v[0];
        for(auto i:v){
            if(cnt==0) cnt=1, ele=i;
            else if(i==ele) cnt++;
            else cnt--;
        }
        cnt=0;
        for(auto i:v){
            if(i==ele) cnt++;
        }
        if(cnt>n/2) return ele;
        return -1;
    }
 ```
> * **Time Complexity:** O(n)
> * **Space Complexity:** O(1)

***



<p id='p6'/>

## 6. Majority Elements 2 (for n/3)
- [Problem 
    <img align="center" height="15" src="https://leetcode.com/_next/static/images/logo-dark-c96c407d175e36c81e236fcfdd682a0b.png">
](https://leetcode.com/problems/majority-element-ii/)
- [Problem 
    <img align="center" height="15" src="https://takeuforward.org/wp-content/uploads/2023/04/Group-11-5.png">
](https://www.codingninjas.com/studio/problems/majority-element-ii_893027)

 **Better Approach**
 ```c++
    vector<int> majority(vector<int>& v) {
        int n=v.size();
        vector<int> ans;
        map<int,int> m;
        for(auto i:v) m[i]++;

        for(auto [k,v]:m){
            if(v>n/2) ans.push_back(k);
        }

        return ans;
    }
 ```
> * **Time Complexity:** O(n.logn)
> * **Space Complexity:** O(n)
---

 **Optimal**
 ```c++
    vector<int> majority(vector<int>& v) {
        int n=v.size(), cnt1=0, cnt2=0, ele1;
        vector<int> ans;
        for(auto i:v){
            if(cnt1==0 && i!=ele2) cnt1=1, ele1=i;
            else if(cnt2==0 && i!=ele1) cnt2=1, ele2=i;
            else if(i==ele1) cnt1++;
            else if(i==ele2) cnt2++;
            else cnt1--, cnt2--;
        }
        cnt1=0, cnt2=0;
        for(auto i:v){
            if(i==ele1) cnt1++;
            else if(i==ele2) cnt2++;
        }
         
        if(cnt1>n/3) ans.push_back(ele1);
        if(cnt2>n/3) ans.push_back(ele2);

        return ans;
    }
 ```
> * **Time Complexity:** O(n)
> * **Space Complexity:** O(1)

***



<p id='p7'/>

## 7. Three Sum
* [Problem 
    <img align="center" height="15" src="https://leetcode.com/_next/static/images/logo-dark-c96c407d175e36c81e236fcfdd682a0b.png">
](https://leetcode.com/problems/3sum/)
* [Problem 
    <img align="center" height="15" src="https://takeuforward.org/wp-content/uploads/2023/04/Group-11-5.png">
](https://www.codingninjas.com/studio/problems/three-sum_6922132)

 **Brute Force**
 ```c++
    vector<vector<int>> threeSum(vector<int>& nums){
        set<vector<int>> s;
        for(int i=0; i<nums.size()-2; i++){
            for(int j=i+1; j<nums.size()-1; j++){
                for(int k=j+1; k<nums.size(); k++){
                    if(nums[i]+nums[j]+nums[k]==0){
                        vector<int> v {nums[i],nums[j],nums[k]};
                        sort(v.begin(),v.end());
                        s.insert(v);
                    }
                }
            }
        }
        vector<vector<int>> ans {s.begin(),s.end()};
        return ans;
    }
 ```
> * **Time Complexity:** O(n^3)
> * **Space Complexity:** O(1)

<!-- >****** -->
---
 **Better One(Hashmap)**
 ```c++
        vector<vector<int>> threeSum(vector<int>& arr) {
        set<vector<int> > s;
        map<int,int> m;
        m[arr[0]]++;
        int n=arr.size();
        for(int i=1; i<n-1; i++){
            for(int j=i+1; j<n; j++){
                int sum=-arr[i]-arr[j];
                if(m.count(sum)){
                    vector<int> v {arr[i],arr[j], sum};
                    sort(v.begin(),v.end());
                    s.insert(v);
                    m[sum]--;
                }
            }
            m[arr[i]]++;
        }

        vector<vector<int>> ans {s.begin(),s.end()};
        return ans;
    }
 ```
> * ***Time Complexity:*** O(n^2)
> * ***Space Complexity:*** O(n)

<!-- ***map o(nlogn)</br>unordered_map o(n^2)*** -->

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

<!-- ***For sorting o(nlogn) & for while loop o(n)*** -->

***



<p id='p8'/>

## 8. Set Matrix Zeroes
* [Problem 
    <img align="center" height="15" src="https://leetcode.com/_next/static/images/logo-dark-c96c407d175e36c81e236fcfdd682a0b.png">
](https://leetcode.com/problems/set-matrix-zeroes/)

 **Optimal Solution**
 ```c++
    void setZeroes(vector<vector<int>>& matrix) {
        unordered_set<int> row, col;
        for(int i=0; i<matrix.size(); i++){
            for(int j=0; j<matrix[i].size(); j++){
                if(matrix[i][j]==0) row.insert(i), col.insert(j);
            }
        }

        for(auto i:col){
            for(int j=0; j<matrix.size(); j++) matrix[j][i]=0;
        }
        for(auto i:row){
            for(int j=0; j<matrix[i].size(); j++) matrix[i][j]=0;
        }
    }
 ```
> * **Time Complexity:** O(mn)
> * **Space Complexity:** O(mn)

<!-- ***For sorting o(nlogn) & for while loop o(n)*** -->

***



<p id='p9'/>

## 9. Spiral Traversal of Matrix
* [Problem 
    <img align="center" height="15" src="https://leetcode.com/_next/static/images/logo-dark-c96c407d175e36c81e236fcfdd682a0b.png">
](https://leetcode.com/problems/spiral-matrix/)

 **Optimal Solution**
 ```c++
   vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int left=0, top=0, right=matrix[0].size()-1, bottom=matrix.size()-1;
        vector<int> ans;
        while(left<=right && top<=bottom){
            for(int i=left; i<=right; i++) ans.push_back(matrix[top][i]);
            top++;

            for(int i=top; i<=bottom; i++) ans.push_back(matrix[i][right]);
            right--;

            if(top<=bottom){
                for(int i=right; i>=left; i--) ans.push_back(matrix[bottom][i]);
                bottom--;
            }

            if(left<=right){
                for(int i=bottom; i>=top; i--) ans.push_back(matrix[i][left]);
                left++;
            }
        }
        return ans;
    }
 ```
> * **Time Complexity:** O(mn)
> * **Space Complexity:** O(mn)

<!-- ***For sorting o(nlogn) & for while loop o(n)*** -->

***

