 we are given a sequence a and b

 b is just a but i = 0, 1, 2 is replaced by a's n-1, n-2

 tgis should be as simple as it can get
 

 ```cpp
void solve()
{
    int n;
    cin>>n;

    vector<int>arr(n);
    for (int i=0; i<n; i++)
    {
        cin>>arr[i];
    }

    int left = 0, right = n-1;

    for (int i = 0; i<n; i++)
    {
        if (i%2==0)
        {
            ans.push_back(arr[left]);
            left++;
        }
        else
        {
            ans.push_back(arr[right]);
            right--;
        }
    }

   cout<<"\n";
}
 ```