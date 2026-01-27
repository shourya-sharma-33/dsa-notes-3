we have x and y
and we choose any prime number p and substract it any number of times from x so x is equal to y

27-n(p) = 5
basically
or p being prime substracted 2 times

basically look into prime factors of  x-y
and u can substract them to get to that

like 27-5=22
22 = 11, 2

27 - 11 - 11 = 5
27 - 2 - 2 - 2 ....... = 5

this is the method

```cpp
void solve(){
    long long x, y;
    cin>>x>>y;

    long long diff = x-y;

    if (diff==1){
        cout<<"NO\n";
    }
    else {
        cout<<"YES\n"
    }
}
```