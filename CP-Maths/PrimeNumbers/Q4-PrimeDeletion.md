u have 9 digit string

and u just have to, without altering the sequence or order
just have to remove

appearing only one time

1234567890
2153467098


it looks very compicated but is way too simple

1 ans 3 would surely exist right
both 13 and 31 are primes

so we will just check what comes first and return 13 and 31 accordingly

```cpp
void solve(){
    string s;
    cin>>s;

    for (int i=0; i<s.length(); i++){
        if(s[i]=='1') {
            cout<<"13"
        } else {
            cout <<"31"
        }
    }
}
```