Its a great way to learn dynamic programming concepts, we will look at three examples and learn all methods

a fibonacci sequece is like it starts with 0 1 and rest are sum of first twoo

so we can see a reccursion type equaltion already with a base case and a reccursion case

0 1 1 2 3 5 8 13 21 34 55

```cpp
int rec(int n){
    if (n==0 || n==1) return n;

    return rec(n-1) + rec(n-2);
}

int fib(int n){
    return rec(n);
}
```

Top Down (Memorization)

in reccursion tree u wll calculate one same reccrusion function multiple times, which is just less efficient so we will just make a vector and we will store it in

say we have calculated fn(5) that is 3

so we save it when we calculate it again for the next time

```cpp
int rec(int n)
{
    if (n==0 || n==1) return n;

    return rec(n-1) + rec(n-2);
}
```



```cpp
int rec(int n, vector<int>&dp)
{
    if (n==0 || n==1) return n;

    if(dp[n]!=-1){
        return dp[n];
    }

    return dp[n] = rec(n-1, dp) + rec(n-2, dp);
}

int fib(int n){
    vector<int>dp(n+1, -1);
    return rec(n, dp);
}
```

Bottom Up (tabulation) 

we dont use reccursion
we just calculate and store in the array luike that


explain chatgpt


```cpp
int fib(int n){
    if (n==0||n==1) return n;
    vector<int>dp(n+1);

    dp[0]=0;
    dp[1]=1;

    for (int i = 2; i<=n; i++)
    {
        dp[i] = dp[i-1] + dp[i-2];
    }

    return dp[i];
}
``` 

Recursion | Memorization | Tabulation 

TC ->  O(2n) | O(n) | O(n) 
SC -> O(1) | O(n) | O(n)

lets see a space optimisation

```cpp
int fib(int n)
{
    if(n==0||n==1) return n;

    int a = 0;
    int b = 1;

    for(int i=2, i<<n; i++)
    {
        int c = a*b;
        a=b;
        b=c;
    }

    return b;
}
```

explain how is it space optimisation chatgpt

