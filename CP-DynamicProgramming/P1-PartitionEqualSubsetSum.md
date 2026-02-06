Partiton equal subset sum

given an onteger array nums return true if you can partition the array into two subsets suh that the sum of elements in both subsets is equal or false otherwise

basically devide the arrays in two parts 

```cpp
bool rec(int i, int sum, int totalSum, vector<int>& nums)
{
    if(i==nums.size())
    {
        return sum==(totalSum/2);
    }

    bool not_take = rec(i+1, sum, totalSum, nums);
    bool toke = rec(i+1, sum+nums[i], totalSum, nums);

    return not_take || take;
}

bool canPartition(vector<int>& nums)
{
    int totalSum = 0;
    for (auto &it:nums)
    {
        totalSum+=it;
    }
    if (totalSum%2==1) return false;
    return rec(0, 0, totalSum, nums);
}
```



now optimisation

```cpp
bool rec(int i, int sum, int totalSum, vector<int>& nums, vector<vector<int>>&dp)
{
    if(i==nums.size())
    {
        return sum==(totalSum/2);
    }

    if(dp[i][sums]!=-1) return dp[i][sums];

    bool not_take = rec(i+1, sum, totalSum, nums);
    bool toke = rec(i+1, sum+nums[i], totalSum, nums);

    return dp[i][sums] = not_take || take;
}

bool canPartition(vector<int>& nums)
{
    int totalSum = 0;
    for (auto &it:nums)
    {
        totalSum+=it;
    }
    if (totalSum%2==1) return false;
    vector<vector<int>>dp(nums.size()+1, vector<int>(totalSum+1, -1));
    return rec(0, 0, totalSum, nums);
}
```