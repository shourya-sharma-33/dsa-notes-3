basically

a slice of array 1 subslice of array 2

basically
```
if a[i] = a[j]
    i++, j++
else
    j++
```

```cpp
void solve()
{
    int n, m;
    cin>>n>>m;

    string a, b;
    cin>>a>>b;

    int i=0, j=0;

    while(i<n && j<m)
    {
        if(a[i]==b[j])
        {
            i++;
            j++;
        }
        else
        {
            j++;
        }
    }

    cout<<i<<"\n"
}

int main()
{
    int t;
    cin>>t;

    while(t--)
    {
        solve();
    }

    return 0;
}
```