remove map and pie from string

tricky part is if we wanna remove map as is it still can form due to surrouding elements

pmapmapie = pie
so do we reiterate multiple times
also if we have mapie?
no
we can just remove a and i from string entiurely

mapie -> remove p
map -> remove a
pie -> remove i

```cpp
void solve()
{
    int n;
    cin>>n;

    string s;
    cin>>s;

    int i = 0;
    int ans = 0;

    while(i<n)
    {
        if(i+5<=n && s.substr(1, 5)=="mapie")
        {
            i+=5;
            ans++;
        }
        else if(i+3<=n && s.substr(i, 3)=="map")
        {
            i+=3;
            ans++;
        }
        else if(i+3<=n && s.substr(i, 3)=="pie")
        {
            i+=3;
            ans++;
        }
        else
        {
            i++;
        }
    }


    cout<<ans<<"\n"
}
```