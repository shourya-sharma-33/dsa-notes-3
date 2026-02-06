S = abzyolfc
T = bzaeoyfl

subsequrce = bzof

```cpp
int rec(int i, int j, string &text1, string &text2)
{
    if(i>=text1.size() || j>=text2.size())
    {
        return 0;
    }

    int ans = 0;

    if(text1[i]==text2[j])
    // if equal we add
    {
        ans = rec(i+1, j+1, text1, text2) + 1;
    }
    else 
    // (explain logic using commnets)
    {
        ans = max(rex(i+1, j, text1, text2), rec(i, j+1, text1, text2));
    }
    return ans;
}

int longestCommonSubsequenc(string text1, string text2)
{
    vector<vector<int>>dp(text1.size(), vector<int>(text2.size(), -1))
    return rec(0, 0, text1, text2);
}
```




```cpp
int rec(int i, int j, string &text1, string &text2)
{
    if(i>=text1.size() || j>=text2.size())
    {
        return 0;
    }

    if(dp[i][j]!=-1) return dp[i][j];

    int ans = 0;

    if(text1[i]==text2[j])
    // if equal we add
    {
        ans = rec(i+1, j+1, text1, text2) + 1;
    }
    else 
    // (explain logic using commnets)
    {
        ans = max(rex(i+1, j, text1, text2), rec(i, j+1, text1, text2));
    }
    return dp[i][j] = ans;
}

int longestCommonSubsequenc(string text1, string text2)
{
    vector<vector<int>>dp(text1.size(), vector<int>(text2.size(), -1))
    return rec(0, 0, text1, text2);
}
```


```cpp
int longestCommonSubsequence (string text1, string text2)
{
    int n = text1.size();
    int m = text2.size();
    vector<vector<int>>dp(n+1, vector<int>(m+1));

    for(int i=0; i<n; i++)
    {
        dp[i][0] == 0;
    }

    for(int i=0; i<m;i++)
    {
        dp[0][i] == 0; 
    }

    for(int i=1; i<=n; i++)
    {
        for(int j=1; j<=m; j++)
        {
            if(text1[i-1]==text2[j-1])
            {
                dp[i][j] = dp[i-1][j-1] + 1;
            }
            else
            {
                dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
            }
        }
    }

    return dp[m][n];
}
```