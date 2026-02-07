this question will more of teach u how to deal

```cpp
void solve(){
    int n;
    cin>>n;

    string s;
    cin>>s;

    set<char<st;
    for(int i = 0; i<n; i++)
    {
        st.insert(s[i]);
    }

    vector<char>v;
    for(auto &it:st)
    {
        v.push_back(it);
    }

    map<char, char>mp;
    for(int i=0; i<v.size(); i++)
    {
        mp[v[i]]=v[v.size()-i-1];
    }

    for(int i=0; i<n; i++)
    {
        cout<<mp(s[i]);
    }

    cout<<"\n";
}
```