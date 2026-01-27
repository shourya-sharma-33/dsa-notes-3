basically

we can sort this and order this descening and find prefix sums

4 3 3 1 1 4 5 9
to
9 5 4 4 3 3 1 1
9 14 18 22 25 28 29 30
and we sum them until they equal to or more than siadn suggar

```cpp
void solve (){
    int n, q;
    cin>>n>>q;

    vector<int>arr(n);
    for (int i=0 ; i<n ; i++){
        cin>>arr[i];
    }

    sort(arr.begin(), arr.end());
    reverse(arr.begin(), arr.end());

    for(int i=1; i<n, i++){
        arr[i]+=arr[i-1];
    }

    while(q--){
        int x;
        cin>>x;
        int lb = lowerBound(arr, n, x);
        lb+=1;

        if(lb>n){
            cout<<"-1\n";
        }
        else{
            cout<<lb<<"\n";
        }
    }

}
```