modular arithmetic

say we have a datatype that has a limit 200

A = 100
B = 200
A + B = Error : Datatype Overflow

or for last digit operations

we can use modulo
we will discuss how it works

some arithmetic operations:

1. (a+b)%m = (a%m + b%m)%m
2. (a-b)%m = (a%m - b%m)%m
3. (a*b)%m = (a%m * b%m)%m

in a way if u look at it

binary exponentations

(a)^b
a= 7
b = 1000000

it ain't feasable
and probably not needed

we can do (7^1000000)%100


also what is binary exponentiation

5^11 = 5^5 * 5^5 * 5
5^5 = 5^2 * 5^2 * 5
5^2 = 5 * 5


and u can see we can apply reccursion

simple solution
```cpp
int findPow(int a, int b){
    int p = 1;

    for (int i=1; i<=b; i++){
        p*=a;
    }

    return p;
}
```


recursive

```cpp
int findPow(int a, int b){
    if (b == 0){
        return 1;
    }

    int x = findPow(a, b/2);
    int ans = 0;

    if (b%2 == 1){
        ans = x*x*a;
    }
    else{
        ans = x*x;
    }
}
```

```cpp
long long finsPowMod (long long a, long long b, long long m){
    if (b == 0){
        return 1;
    }
    if(b == 1){
        return a;
    }

    long long x = findPowMod(a, b/2, m)%m;
    long long ans=0;

    if(b%2==1){
        ans = (x%m + x%m)%m;
        ans = (ans%m + a%m)%m;
    }
    else{
        ans = (x%m + x%m)%m;
    }

    return ans;
}
```

