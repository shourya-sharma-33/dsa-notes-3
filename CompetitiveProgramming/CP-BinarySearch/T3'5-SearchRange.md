range is set of all numbers btween upper and lower bound

```cpp
vector<int> searchRange(vector<int>& nums, int target){
    int n = nums.size();
    int lb = lowerBound(nums, n, target); // already written
    int ub = upperBound(nums, n , target);

    if (lb == ub){
        return {-1, -1};
        //not present
    }
    else {
        return {lb, ub - 1};
    }
}
```

we also have these functions in standard library

lower_bound(nums.begin(), nums.end(), target);