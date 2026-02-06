thrre is a grid with H orizontal rows and w vertical clumn let (i, j) donate the square at the ith row from the top and the jth colum for th eleft for each i and k (1<i<H and 1<j<w) square (i, j) is desctibe by a character a ij and if a ij is square (i, j) is an empty square if a ij is # is a wall square it is guaanteed that squares(1,1) and (h,w) are eptu sqaures

taro will starts for square (1,1) and reach(H, W) by repeatedly moving right or down to an adjacent empty square

find the number o taro's paths from square (1, 1) to (h, w) as the answer can be extremely large so find modulo

```cpp
int rec(int i, int j, int n, int m vector<string>&matrix)
{
    if((i==n-1) && (j==m-1))
    {
        return 1;
    }

    if(i>=n || j>=m || matrix[i][j]=='#')
    {
        return 0;
    }

    int mod = 100000007

    int right = rec(i, j+1, n, m, matrix)%mod;
    int bottom = rec(i+1, j, n, m, matrix)%mod;

    return (right+bottom)%mod;
}

void solve()
{
    int n, m;
    cin>>n>>m;

    vector<string>matrix[i];

    int ans = rec(0, 0, n, m, matrix);
    cout<<ans<<"\n";
    
}
```


```cpp
int rec(int i, int j, int n, int m vector<string>&matrix, vector<vector<int>>&dp)
{
    if((i==n-1) && (j==m-1))
    {
        return 1;
    }

    if(i>=n || j>=m || matrix[i][j]=='#')
    {
        return 0;
    }

    if(dp[i][j]!=-1)return dp[i][j];

    int mod = 100000007

    int right = rec(i, j+1, n, m, matrix, dp)%mod;
    int bottom = rec(i+1, j, n, m, matrix dp)%mod;

    return dp[i][j] = (right+bottom)%mod;
}

void solve()
{
    int n, m;
    cin>>n>>m;

    vector<string>matrix[i];

    int ans = rec(0, 0, n, m, matrix);
    cout<<ans<<"\n";
    
}
```

