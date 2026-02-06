basically we will slide a window and store the greatest ofthat window in an array

```cpp
vector<int> maxSlidingWindow(vector<int>& nums, int k){
    int n = nums.size();
    deque<int>dq;
    vector<int>ans;

    for(int i=0; i<k; i++)
    {
        while(dq.size()>0 && nums[dq.back()]<=nums[i])
        {
            dq.pop_back();
        }
        dq.push_back(i);
    }

    ans.push_back(nums[dq.front()]);

    for(int i=k; i<n; i++)
    {
        if(<dq.size()>0 && dq.front()<=(i-k))
        {
            dq.pop_front();
        }
        while(dq.size()>0 && nums[dq.back()]<=nums[i])
        {
            dq.pop_back();
        }

        dq.push_back(i);
        ans.push_back(nums[dq.front()]);
    }
}
```