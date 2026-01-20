# Basic Maths (C++ Notes)

## 1. Digit Extraction

Given a number
`n = 7789`

Digits needed → `9, 8, 7, 7`

### Logic

* **Last digit** of a number = `n % 10`
* **Remove last digit** = `n / 10`
* Repeat until `n > 0`

### Example

```
7789 % 10 = 9
778  % 10 = 8
77   % 10 = 7
7    % 10 = 7
```

---

## 2. Count Digits in a Number

### Logic

* Keep dividing by `10`
* Count how many times until `n` becomes `0`

### Code

```cpp
int countDigits(int n){
    int cnt = 0;
    while(n > 0){
        cnt++;
        n = n / 10;
    }
    return cnt;
}
```

---

## 3. Reverse a Number

### Logic

* Extract last digit
* Push it into reverse number using `rev = rev * 10 + digit`

### Code

```cpp
int main(){
    int n;
    cin >> n;

    int revNum = 0;
    while(n > 0){
        int ld = n % 10;
        revNum = revNum * 10 + ld;
        n = n / 10;
    }

    cout << revNum;
}
```

---

## 4. Palindrome Number

A number is **palindrome** if:

```
original number == reversed number
```

### Logic

* Store original number
* Reverse it
* Compare

### Code

```cpp
bool isPalindrome(int n){
    int temp = n;
    int rev = 0;

    while(n > 0){
        int ld = n % 10;
        rev = rev * 10 + ld;
        n /= 10;
    }

    return rev == temp;
}
```

---

## 5. Armstrong Number

A number is **Armstrong** if:

```
sum of (each digit ^ number of digits) == number
```

### Example

```
371 = 3³ + 7³ + 1³
```

### Logic

* Count digits
* Extract each digit
* Raise to power
* Add to sum

### Code

```cpp
bool isArmstrong(int n){
    int temp = n;
    int sum = 0;
    int digits = countDigits(n);

    while(n > 0){
        int ld = n % 10;
        sum += pow(ld, digits);
        n /= 10;
    }

    return sum == temp;
}
```

---

## 6. Print Divisors (Brute Force)

### Logic

* Loop from `1` to `n`
* If `n % i == 0`, print `i`

### Code

```cpp
for(int i = 1; i <= n; i++){
    if(n % i == 0){
        cout << i << " ";
    }
}
```

---

## 7. Print Divisors (Optimized)

### Logic

* Loop till `sqrt(n)`
* Print `i` and `n/i`
* Avoid duplicates

### Code

```cpp
vector<int> divisors;

for(int i = 1; i * i <= n; i++){
    if(n % i == 0){
        divisors.push_back(i);
        if(n / i != i)
            divisors.push_back(n / i);
    }
}

sort(divisors.begin(), divisors.end());
```

---

## 8. Prime Number Check

A number is **prime** if:

```
exactly 2 factors → 1 and itself
```

### Brute Force

```cpp
bool isPrime(int n){
    if(n <= 1) return false;

    int cnt = 0;
    for(int i = 1; i <= n; i++){
        if(n % i == 0)
            cnt++;
    }
    return cnt == 2;
}
```

### Optimized (√n)

```cpp
bool isPrime(int n){
    if(n <= 1) return false;

    for(int i = 2; i * i <= n; i++){
        if(n % i == 0)
            return false;
    }
    return true;
}
```

---

## 9. GCD / HCF (Brute Force)

### Logic

* Loop from `1` to `min(n1, n2)`
* Last divisor that divides both is GCD

### Code

```cpp
int gcd(int a, int b){
    int ans = 1;
    for(int i = 1; i <= min(a, b); i++){
        if(a % i == 0 && b % i == 0)
            ans = i;
    }
    return ans;
}
```

---

## 10. Euclidean Algorithm (Optimized GCD)

### Formula

```
gcd(a, b) = gcd(a % b, b)
```

### Logic

* Keep reducing larger number
* Stop when one becomes `0`

### Code

```cpp
int gcd(int a, int b){
    while(a > 0 && b > 0){
        if(a > b)
            a = a % b;
        else
            b = b % a;
    }

    if(a == 0) return b;
    return a;
}
```

