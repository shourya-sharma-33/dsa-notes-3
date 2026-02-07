you are a professional robber planning to rob houses along a street each house has a certain amount of money stashed thw only consraint stopping you from robbing each of them is that adjacent houses habe a securtu systems connected and it will automatically contct the police if two adjacent houses were broken into on the same night

given an integer array nums representing the amojnt od money of each house return the maximum amount of money you can rob tonight without aerting the police

\we use the same method

```cpp
int rec(int i, vector<int>& nums)
{
    // Base Case
    if(i>=nums.size())
    {
        return 0;
    }

    // Not Take Case
    int not_take = rec(i+1, nums);

    // Take Case
    int take = nums[i] + rec(i+2, nums);

    return max(not_take, take);
}

int rob(vector<int>& nums)
{
    return rec(0, nums);
}
```


```cpp
int rec(int i, vector<int>& nums, vector<int>&dp)
{
    // Base Case
    if(i>=nums.size())
    {
        return 0;
    }

    if(dp[i]!=-1) return dp[i];
    // Not Take Case
    int not_take = rec(i+1, nums);

    // Take Case
    int take = nums[i] + rec(i+2, nums);

    return dp[i] = max(not_take, take);
}

int rob(vector<int>& nums)
{
    vector<int>dp(nums.size(), -1);
    return rec(0, nums);
}
```
