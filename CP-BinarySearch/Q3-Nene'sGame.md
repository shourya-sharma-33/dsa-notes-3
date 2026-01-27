basically the game will work like this

4 6 7 9
a b c d e f g h i
a b c e h
a b c h
a b c
terminated lower than 4

a b c is the answer

but we really just have to find out the number of players in the end

so the simpler solution would be

9 - 4 = 5
5 - 1 = 4
4 - 1 = 3

this is a simpler way
we are checking in a perticular round how many players are being removed

basically this is how it will work

+--+--+--+--+
|1 |2 |3 |4 |
+--+--+--+--+
|3 |6 |7 |9 |
+--+--+--+--+

now number of players are 10
9 - 4 = 5
5 is lower bound of 4
4's index is 1
5 - 1 is 4
4 is lower bound of 4
4's index is 1
4 - 1 is 3



```cpp
void solve(){
    int k, q;
    cin>>k>>q;

    vector<int>a[k];
    for(int i = 0; i<k ; i++){
        cin>>a[i];
    }

    while(q--){
        int n;
        cin>>n;
        cout<<min(a[0]-1, n)<<"\n";
    }
}

```