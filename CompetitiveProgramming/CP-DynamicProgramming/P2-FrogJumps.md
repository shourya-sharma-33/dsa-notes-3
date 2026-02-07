There are n stones numbered 1 2 .... n for each i (i<i<n) the height of stone i is h


there isa frog who is initially on stone 1, he will repeart the following action some numbers of times to reach stone n

if the frog is currently on stone 1
he will repeat the following action some numbers o times to rach stone n


basially its the same ass problem


```cpp

int rec(int i, vector<int>&heights)
{
    if(i==heights.size())
    {
        return 0;
    }

    int one_step = abs(heights[i] - heights[i-1]) + rec(i+1, heights);
    
    int two_step = INT_MAX;
    if(i<(heights.size()-2))
    {
        two_step = abs(heights[i]-heights[i+2]) + rec(i+2, heights);
    }

    return min(one_step, two_step);
}
void solve()
{
    int n;
    cin>>n;

    vector<int>heights(n);
    for(int i=0;i<n;i++)
    {
        cn>>heights[i];
    }

    int ans = rec(0, heights);
    cout<<ans<<"\n";
}

```



```cpp

int rec(int i, vector<int>&heights, vector<int>&dp)
{
    if(i==heights.size())
    {
        return 0;
    }

    if(dp[i]!=-1) return dp[i];

    int one_step = abs(heights[i] - heights[i-1]) + rec(i+1, heights);
    
    int two_step = INT_MAX;
    if(i<(heights.size()-2))
    {
        two_step = abs(heights[i]-heights[i+2]) + rec(i+2, heights);
    }

    return dp[i] = min(one_step, two_step);
}
void solve()
{
    int n;
    cin>>n;

    vector<int>heights(n);
    for(int i=0;i<n;i++)
    {
        cn>>heights[i];
    }

    vector<int>dp(n, -1);

    int ans = rec(0, heights, dp);
    cout<<ans<<"\n";
}

```




```cpp

int rec(int i, vector<int>&heights, vector<int>&dp)
{
    if(i==heights.size())
    {
        return 0;
    }

    if(dp[i]!=-1) return dp[i];

    int one_step = abs(heights[i] - heights[i-1]) + rec(i+1, heights);
    
    int two_step = INT_MAX;
    if(i<(heights.size()-2))
    {
        two_step = abs(heights[i]-heights[i+2]) + rec(i+2, heights);
    }

    return dp[i] = min(one_step, two_step);
}
void solve()
{
    int n;
    cin>>n;

    vector<int>heights(n);
    for(int i=0;i<n;i++)
    {
        cn>>heights[i];
    }

    if (n==1) 
    {
        cout<<"0\n";
        return;
    }

    vector<int>dp(n);

    dp[0] = 0;
    dp[1] = abs(heights[1] - heights[0]);

    for(int i=2; i<n; i++)
    {
        int last = dp[i-1] + abs(heights[i-1]-heights[i]);
        int lastSecond = dp[i-2] + abs(heights[i-2]-heights[i]);

        dp[i] = min(last, lastSecond);

    }
    
    cout<<dp[n-1]<<"\n";
}

```
