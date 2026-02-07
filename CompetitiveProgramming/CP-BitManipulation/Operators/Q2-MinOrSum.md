we have to replace any two number with any two number
the or of both number should be eqal to replsced numbrts

and in such a way that the sum of array is minimum

lets take any two numbers 
20 : 10100
17 : 10001
20|17 : 10101 = 21

basically we can replace with 21|0


so we will take or of whole array and replace

```cpp
void solve(){
    int n;
    cin>>n;
    int x = 0;
    for (int i=0; i<n : i++){
        int y;
        cin>>y;
        x|=y;
    }

    cout<<x<<"\n"
}

int main(){
    int t;
    cin>>t;

    while(t--){
        solve();
    }

    return 0;
}
```