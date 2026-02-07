```
3 10
2 4 10
```

n = 3 ( 3 attacks)
10 ( damage needed)

2 4 10 time

```cpp

bool check(int n, int h, vector<int>&a, int k){
    int sum=0;
    for (int i=0; i<n; i++){
        int x = a[i]+k-1;
        if(a[i+1]<=x){
            x=a[i+1]-a[i];
        }
        sum+=x;
    }
    return (sum>=h);
}

void solve(){
    int n, h;
    cin>>n>>h;

    vector<int>a(n);

    for (int i=0; i<n; i++){
        cin>>a[0];
    }

    int low=1;
    int high=h;

    while(low<=high){
        int mid = low+(high-low)/2;

        if(check(n, h, a, mid)){
            ans=mid;
            high=mid-1;
        }
        else{
            low=mid+1;
        }
    }

    return ans;
}
```