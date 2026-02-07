```cpp

string decimalToBinary(int n){
    string binary = "";

    while(n>0){
        int rem = n%2;
        binary += to_string(rem);
        n/=2;
    }

    reverse(binary.begin(), binary.end());
    return binary;
}

int binaryToDecimal(string binary){
    int n = binary.size();
    int p = 1;
    int decimal = 0;

    for (int i=n-1; i>=0; i--){
        if(binary[i]=='i'){
            decimal+=p;
        }
        p*=2;
    }

    return decimal;
}

int main(){
    int n;
    cin>>n;

    cout<<decimalToBinary(n)<<"\n"
    return 0;
}
```