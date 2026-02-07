basically we have two number and n and k

we want a fibonacci in such a way that the number n is on kth position

say n= 22 k = 4

so

6 8 14, 22
4 9 13 22
2 10 12 22
0 11 11 22

```cpp
void solve ()
{
    long n, k;
    cin>>n>>k;

    for (int i=0; i<=n; i++)
    {
        vector<int>dp(k+1);
        dp[k]=n;
        dp[k-1]=i;

        for (int j=k-2; j>=1; j--)
        {
            dp[j] = dp[j+2]-dp[j+1];
            if(dp[j]>dp[j+1])
            {
                isValid=false;
                break;
            }
            if(dp[j]<0)
            {
                isValid=false;
                break;
            }
        }

        if(isValid)
        {
            ans++;
        }
    }

    cout<<ans<<"\n";
}
```


well what we are doing is we start

we start : n 0 n
now we know that the n+1th char should we greater than n

so we loop and verify
we go in the inner loop only when 1th index is gretater than 0th


and then  we keep verifying and appending the ans

