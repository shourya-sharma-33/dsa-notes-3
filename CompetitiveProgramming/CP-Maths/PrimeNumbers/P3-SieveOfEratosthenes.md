this is a great method to find prime numbers in a 1 -> n
and we will understand the work process

we will make a vector only contianing trues
(fill with )
+-----+-----+-----+-----+-----+-----+-----+-----+-----+-----+
| 0 T | 1 T | 2 T | 3 T | 4 T | 5 T | 6 T | 7 T | 8 T | 9 T |
+-----+-----+-----+-----+-----+-----+-----+-----+-----+-----+
| 10T | 11T | 12T | 13T | 14T | 15T | 16T | 17T | 18T | 19T |
+-----+-----+-----+-----+-----+-----+-----+-----+-----+-----+
| 20T | 21T | 22T | 23T | 24T | 25T | 26T | 27T | 28T | 29T |
+-----+-----+-----+-----+-----+-----+-----+-----+-----+-----+
| 30T | 31T | 32T | 33T | 34T | 35T | 36T | 37T | 38T | 39T |
+-----+-----+-----+-----+-----+-----+-----+-----+-----+-----+-----+
| 40T | 41T | 42T | 43T | 44T | 45T | 46T | 47T | 48T | 49T | 50T |
+-----+-----+-----+-----+-----+-----+-----+-----+-----+-----+-----+

this is what we have 
now we pass this to what seems like a seive

1. 0 and 1 are flipped false  right off the bat
2. all even number except 2 are flipped
3. and now we run a loop on all true values and divide them with i = 2, 3, 4, ---- n

basically now we running the loop on lesser numbers

```cpp
vector<bool> sieve(int n){
    vector<bool>primes(n+1, true);

    primes[0]=false;
    primes[1]=false;

    for(int i=2; i*i<=n; i++){
        if(primes[i] == true){
            for(int j = i*i; j<=n ; j+=i){
                prime[j]=false;
            }
        }
    }
    return primes;
}
```

this is time complexity
(n/2 + n/3 --------)
= n (1/2 + 1/3 + ------)
= n(log2(log2(n)))


this is way better than n(sqrt(n))