basically we are raising some bacteria

we already have some bacteria
we have to minimise the amount of bactria used
first day we place 1 bacteria
we wait
1 turned to 2
2 to 4
4 to 8
8 -> 16

we dont want 32 only x = 23
16 + 7 = 23
but bateria we used is 8

now we add one bacteria each day
1 -> 2
2 + 1 = 3 -> 6
6 + 1 = 7 -> 14
14 -> 28

now

1 -> 2 -> 4 + 1 = 5 -> 10 + 1 = 11 -> 22 + 1 = 23


how do we solve this
bacteria are doubling in power of two

we want 23 bacteria
meaing
10111 
2^0= 1
1 x 2 + 1 = 2 + 1 = 3

```cpp
int countSetBits(int n){
    int count = 0;
    while(n){
n=n&n-1;
count++
    }
    return couny
}
int main(){
    long long x;
    cin>>x;

    cout<<countSetBits(x);
    return 0;
}
```