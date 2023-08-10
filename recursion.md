# Notes on Recursion

## Print 1 to N
```c++
void print_n (const int n) {
    if (n == 1){
        cout << "1" << '\n';
        return;
    }
    cout<< n <<" ";
    print_n(n-1);
};
```

## Print N to 1
```c++
void print_n (const int n) {
    if (n == 1){
        cout << "1" << '\n';
        return;
    }
    print_n(n-1);
    cout<< n <<" ";
};
```