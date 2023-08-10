# Basic Problem with Array

- [Easy](#easy)
    - [1. Remove Duplicate](#p1)
    - [2. Rotate an Array to left by 'd' steps](#p2)
    - [3. Move all zero to the end of Array](#p3)
    - [4. Union of 2 sorted Array](#p4)
    - [5. Intersection of 2 sorted Array](#p5)
    - [6. Find missing number](#p6)
    - [7. Maximum subarray sum](#p7)
    - [8. Longest Subarray with given Sum K](#p8)
- [Medium](#medium)
- [Hard](#hard)

<a id="easy"></a>

- <p id='p1'/>
## 1. Remove Duplicate 
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


- <p id='p2'/>
## 2. Rotate an Array to left by 'd' steps

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


- <p id='p3'/>
## 3. Move all zero to the end of Array

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


- <p id='p4'/>
## 4. Union of 2 sorted Array

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


- <p id='p5'/>
## 5. Intersection of 2 sorted Array

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


- <p id='p6'/>
## 6. Find missing number

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


- <p id='p7'/>
## 7. Maximum subarray sum

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

>***Here summation may be overflow for large integer, xor method is more optimal solution than the first one***
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

>***Here summation may be overflow for large integer, xor method is more optimal solution than the first one***

***


- <p id='p8'/>
## 8. Longest Subarray with given Sum K
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

>***Here summation may be overflow for large integer, xor method is more optimal solution than the first one***

***



<div id="medium"/>








<div id="hard"/>