how to calculate sqrt of a number
there are multiple possible algoritthms for it

unlike multiplication
u cant say
find x so that x*x is 25
and just find it out

out of thoose algorithms one uses binary search

we know sqrts are always smaller than thenumber itself

what we can do it
we can look for the number between them

```cpp
int mySqrt(int x){
    if (x==0) return 0;
    int low = 0;
    int high = x;

    while (low <= high){
        long mid = (low+high)/2;
        long midsquare = mid*mid;

        if (midsqare>x){
            high = mid - 1;
            
        }
    }
}
```