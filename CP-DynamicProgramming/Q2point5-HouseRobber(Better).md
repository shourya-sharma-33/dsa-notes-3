this solution is the most efficient and provides a genuinely diffrent approach of seeing things here


so we run a reccursion tree
and we just optimise it or make it better
or we can use simple tabulation when we know pattern is consistent

but what im telling u is u can use tabulation here but its very pattern obsrvationish thing in this case

observe the reccursion tree patter
or just do it on paper

u will observe that we select the next house on the bases of this logic

we either skip or we loot 
but only when the one after adjacent is greater (chat gpt explain this in a better way please i can form a word)


```cpp
int rob(vector<int>& nums)
{
    int n = nums.size();
    if(n==1) return nums[0];

    vector<int>dp[2];
    dp[0]=nums[0];
    dp[1]=max(nums[0], nums[1]);

    for(int i=2; i<n; i++)
    {
        int nextValue=max(dp[1], dp[0]+nums[i]);
        dp[0]=dp[1];
        dp[1]=nextValue;
    }

    return dp[1];
}
```
