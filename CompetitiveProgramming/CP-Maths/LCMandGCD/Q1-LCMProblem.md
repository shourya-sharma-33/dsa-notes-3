let lcm(x, y) be the minimum positive integer that is divisible by both x and y


you are given two integger l and r find two inteeger x and y such that l <= x < y <= r  and l<= lcm(x, y) <= r

solution is that if y*2 more than r than no sliution else the slution will be l and 2l
(chatgpt explain how that works)

```cpp
void solve(){
    long long l, r;
    cin>>l>>r;

    long long x = l;
    long long y = 2*l;

    if(y<=r){
        cout<<x<<""<<y<<"\n";
    }
    else{
        cout<<"-1 -1\n"
    }
}
```