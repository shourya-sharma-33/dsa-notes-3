lower bound is : write chatgpt
upper bound is : write chatgpt

```cpp
int lowerBound(vector<int>& nums, int n, int target){
    int l = 0;
    int r = n-1;
    int ans =n;

    while (l<=r){
        int mid = (l+r)/2;
        if (arr[mid]>= target){
            ans = min(ans, mid);
            r = mid-l;
        }
        else {
            l = mid + l;
        }
    }

    return ans;
}
```

also write one for upper bound