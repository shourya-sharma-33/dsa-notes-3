you are given a playlist of a radio station since its establishment the playlist has a total of n songs

whta is the longest sequence fof successive songs where each song is unique

simple 

1 2 1 3 2 7 4 2

obviously is : 7 4 2

```cpp
int main()
{
    int n;
    cin>>n;

    vector<long>v(n);
    for (int i=0; i<n; i++)
    {
        cin>>v[i];
    }

    map<long, long>mp;
    int i=0, j=0;
    int ans = 1;

    mp[v[0]]++;

    while(j<(n-1))
    {
        j++;
        while(mp[v[j]]>0)
        {
            mp[v[i]]--;
            i++;
        }
        mp[v[j]]++;
        ans=max(ans, j-i+1);
    }
    cout<<ans<<"\n";
    return 0;
}
```