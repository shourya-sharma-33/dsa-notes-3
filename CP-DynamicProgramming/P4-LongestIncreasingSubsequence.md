nums = [5, 3, 7, 6]
arr = [3, 7]


```cpp
int rec(int currIndex, int prevIndex, int n, vector<int>& nums)
{
    if(currIndex==n) return 0;

    int not_take = rec(currIndex+1, prevIndex, n, nums);

    int take = INT_MIN;
    if(prevIndex==-1 || nums[currIndex]>nums[prevIndex])
    {
        take = 1 + rec(currIndex+1, currIndex, n, nums);
    }

    return max(not_take, take);
}

int lengthOfLIS(vector<int>& nums)
{
    int n = nums.size();
    return rec(0, -1, n, nums);
}
```


```cpp
int rec(int currIndex, int prevIndex, int n, vector<int>& nums)
{
    if(currIndex==n) return 0;

    if(dp[currIndex][prevIndex+1]!=-1)
    {
        return dp[currIndex][prevIndex+1];
    }

    int not_take = rec(currIndex+1, prevIndex, n, nums);

    int take = INT_MIN;
    if(prevIndex==-1 || nums[currIndex]>nums[prevIndex])
    {
        take = 1 + rec(currIndex+1, currIndex, n, nums);
    }

    return max(not_take, take);
}

int lengthOfLIS(vector<int>& nums)
{
    int n = nums.size();
    vector<vector<int>>dp(n+1, vector<int>(n+1, -1));
    return rec(0, -1, n, nums);
}
```
