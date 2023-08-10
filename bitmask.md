# Bit Manipulation

## Count Set Bit
```cpp
int countSetBit(int n) {
    int cnt = 0;
    while (n > 0){
        if (1 & n) ++cnt; 
        n >>= 1; // shift right by one bit until n becomes 0
    }
}
```
**Time Complexity: O(log2(n))**

---

```cpp
int countSetBit(int n) {
    int cnt = 0;
    while (n > 0){
        cnt++;
        n = n&(n-1);
    }
}
```
**Time complexity : O(cnt)**
where cnt is the number of set bits in `n`

---

Defualt Method
```cpp
int cnt=__builtin_popcount(n);
```
---

* [Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)
* [Counting Bits](https://leetcode.com/problems/counting-bits/description/)

***


## [Power of Tow](https://leetcode.com/problems/power-of-two/description/)
8-->(1000) is power of 2 and 7-->(111)\
8 & 7 = 0


```c++
bool isPowerOfTwo(long long n) {
    if(n<=0) return 0;
    return !n&(n-1);
}
```

***


## [XOR Queries of a SubArray](https://leetcode.com/problems/xor-queries-of-a-subarray/)
- **Basic Properties**
    - A^0=A
    - A^A=0
    - 10101 ^ 11011=01110
    - 1^2^3==3^1^2 (Order doesn't matter.)

```c++
vector<int> xorQueries(vector<int>& arr, vector<vector<int>>& q) {
    int n=arr.size();
    vector<int> pre (n+1), ans(q.size());
    // Prefix XOR
    for(int i=1; i<=n; i++) pre[i]=pre[i-1]^arr[i-1];

    for(int i=0; i<q.size(); i++){
        int L=q[i][0], R=q[i][1]+1;
        ans[i]=pre[R]^pre[L];
    }
    return ans;
}
```



<!-- ## Reverse Bits
of a Number
.
```cpp
unsigned reverseBits(uint32_t x, unsigned numbits=sizeof(x)*
8);
{
    uint32_t result = 0;
    for (;numbits>0;)
     -->