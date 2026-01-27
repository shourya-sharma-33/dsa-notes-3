situation is

p1[w1, w2] p2[w2 ---------- w9] p3[w10 ----- w12] p4[w13 ----- w16] p5 [w17 ----- w25]

arr = 2, 7, 3, 4, 9
prefixSum = 2, 9, 12, 16, 25

say we need to find in which pile is worm14

we can find its lower bound in the prefixSumArray 

```cpp
int main(){
    int n;
    cin>>n;

    vector<int>arr(n);
    for(int i=0; i<n; i++){
        cin>>arr[i];
    }
    
    // prefix sum array
    for(int i=1; i< n; i++){
        arr[i] += arr[i-1];
    }

    int m;
    cin>>m;

    while(m--){
        int q;
        cin>>q;

        int lb = lowerBound(arr, n, q) + 1;
        
        cout<<lb<<"\n"
    }

    return 0;
}
```