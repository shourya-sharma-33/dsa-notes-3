a string is good if no rpeated characters

```cpp
int countGoodSubStrings(string s)
{
    map<char, int>mp;
    int n = s.size();

    for (int i=0; i<3; i++)
    {
        mp[s[i]]++;
    }

    int i = 0;
    int j = 2;

    while(j<n)
    {
        j++;
        mp[s[j]]++;
        mp[s[i]]--;
        i++;
        bool ok = true;
        for (auto &it:mp)
        {
            if(it.second>1)
            {
                ok = false;
            }
        }
        if (ok==true)
        {
            ans++;
        }
    }


}
```