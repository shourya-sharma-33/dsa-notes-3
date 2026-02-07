Knap sack 


problem statememnt:
u have a knapsack (thaila in hindi) that has a capacity of 12 kg

and we have 5 items with a w and a v parameter 


we have to make sure we keep the knapsack tact (equal to or less than capacity) and keep the max value

say we have a

w = 3 4 8 1
v = 20 12 10 21

so if caoacity is 10
we can choose
8 only
ot we can take 3 + 4 + 1
wgich i better
now


there is not really any algorithm we can write for this
not some special algorithm basically just simple brite force type solution

we can optimise with tabulation and memorisation
but we would stil use a recursion case, with a take not take type scenario

```cpp
long rec(int i, int W, int n, vector<int>&v, vector<int>&w)
{
    // Base Case
    if(i==n)
    {
        return 0;
    }

    // not take
    long not_take= rec(i+1, W, n, v, w);

    long take = INT_MIN;

    if (w[i]<=W)
    {
        take = v[i]+rec(i+1, W-w[i], n, v,w);
    }

    return max(take, not_take);
}


void solve()
{
    long n, w;
    cin>>n>>w;

    vector<int>v(n);
    vector<int>w(n);

    for (int i=0; i<n; i++)
    {
        cin>>w[i]>>v[i];
    }

    long ans = rec(0, W, n, v, w); 
    cout<<ans<<"\n";
    
}

int main()
{
    solve();
    return 0;
}
```


memorisation

```cpp
long rec(int i, int W, int n, vector<int>&v, vector<int>&w, vector<vector<long>>&dp)
{
    // Base Case
    if(i==n)
    {
        return 0;
    }

    if(dp[i][W]!=-1)
    {
        return dp[i][W];
    }

    // not take
    long not_take= rec(i+1, W, n, v, w);

    long take = INT_MIN;

    if (w[i]<=W)
    {
        take = v[i]+rec(i+1, W-w[i], n, v,w);
    }

    return dp[i][W] = max(take, not_take);
}


void solve()
{
    long n, w;
    cin>>n>>w;

    vector<int>v(n);
    vector<int>w(n);

    for (int i=0; i<n; i++)
    {
        cin>>w[i]>>v[i];
    }

    // vector for memorisation
    vector<vector<int>>dp(n+1, vector<long>(W+1, -1));

    long ans = rec(0, W, n, v, w); 
    cout<<ans<<"\n";
    
}

int main()
{
    solve();
    return 0;
}
```