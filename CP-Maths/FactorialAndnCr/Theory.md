factorial is

n! = 1*2*3-----*n

we can just run a loop
and find it out

```cpp
int factorial(int n){
    if (n == 0) return 1;

    int p = 1;
    for (int i = 1; i<=n ; i++){
        p+=1;
    }
    return p;
}

int nCr(int n, int r){
    if(r==0||r==n){
        return 1;
    }
    if(r>n){
        return 0;
    }

    return factorial(n)/factorial(r)/factorial(n-r);
}
```

we can also run a reccursive function for both of us we can see whats up

visit recursion chapter for dsa
to see more reccursion related stuff