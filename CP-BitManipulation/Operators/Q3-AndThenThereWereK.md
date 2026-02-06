basically we have to find k
so that
(n)&(n-1)&(n-2)&...........(k) = 0

```cpp
void solve(){
    long long n;
    cin>>n;

    int x = n;

    while (x>0){
        n-=1;
        x&=n;
    }
    cout<<n<<"\n"
}
```

a better approach
(please explain this approach)

```cpp
void solve (){
    long long n;
    cin>>n;
    int c=0;

    while (n>0){
        n>>=1;
        c++;

    }

    int ans = (1<<(c-1))-1;
    cout<<ans<<"\n";
}


```