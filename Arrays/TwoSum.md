# Brute Force Solution

Iterate over list and check all pairs if sum is possible if yes then return indices of pair.

| Time Complexity | Space Complexity : |
| :-------------: | :----------------: |
|    $O(n^2)$     |       $O(1)$       |

## Code

```
    vector <int> ans;
        for(int ptrA = 0 ; ptrA < nums.size() ; ptrA++)
        {
            for(int ptrB = ptrA+1 ; ptrB < nums.size() ; ptrB++)
            {
                if(nums[ptrA]+nums[ptrB] == target)
                {
                    ans.push_back(ptrA);
                    ans.push_back(ptrB);
                    break;
                }
            }
            if(ans.size())
                break;
        }
    return ans;
```

<hr>

# Best Solution - 1 (Hashing)

### Approach

- Create a hash map and store the occuring elements in it.
- If first element is `x` then other element should be `sum-x`.
- Using this logic we check for every index if current element is x and if `hashmap[sum-x] > 0` thus answer possible.
- Remember to not use x = sum/2.

| Time Complexity | Space Complexity : |
| :-------------: | :----------------: |
|     $O(n)$      |       $O(n)$       |

## Code

```
    vector<int> res;
        int n = nums.size();
        unordered_map <int,int> hash;
        for(int i = 0 ; i < n ; i++)
        {
            if(i > 0 && hash[target - nums[i]] > 0)
            {
                res.push_back(hash[target-nums[i]] - 1);
                res.push_back(i);
                break;
            }
            hash[nums[i]] = i + 1;
        }
    return res;
```

<hr>

# Best Solution - 2 (Sorting & Binary Search)

- Sort the array. for every element `a[i]` check if `sum - a[i]` exists using binary search.
- if Yes return the indices.

| Time Complexity | Space Complexity : |
| :-------------: | :----------------: |
|   $O(nlogn)$    |       $O(n)$       |

## Code

```
    int n = nums.size();
    vector<pair<int,int>> p(n);
    for(int i = 0 ; i < n ; i++)
        p[i] = {nums[i],i};
    sort(nums.begin(),nums.end());
    sort(p.begin(),p.end());
    vector<int> res;
    for(int i = 0 ; i < n-1 ; i++)
    {
        if(binary_search(nums.begin()+i+1,nums.end(),target-nums[i]))
            {
                res.push_back(p[i].second);
                int idx = lower_bound(nums.begin()+i+1,nums.end(),target-nums[i]) - nums.begin();
                res.push_back(p[idx].second);
                break;
            }
    }
    return res;
```
