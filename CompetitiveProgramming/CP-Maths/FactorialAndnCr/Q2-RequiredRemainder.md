u need to fins maaximum integer l such that 

k mod x = y
0=<k=<n

x, y, n need to find maximum possoble integer from - to n that has the remainder y%x

```cpp
void solve (){
    int x, y, n;

    cin>>x>>y>>n;

    int k = (n/x)*x;
    k+=y;

    if(k>n){
        k-=x;
    }

    cout<<k<<"\n"
}
```