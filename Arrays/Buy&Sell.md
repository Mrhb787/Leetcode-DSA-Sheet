# Brute Force Solution

Iterate over list and check all pairs to find the pair with maximum difference.

| Time Complexity | Space Complexity : |
| :-------------: | :----------------: |
|    $O(n^2)$     |       $O(1)$       |

## Code

```
    int profit = 0;
        for(int ptrA = 0 ; ptrA < prices.size() ; ptrA++)
        {
            for(int ptrB = ptrA+1 ; ptrB < prices.size() ; ptrB++)
            {
                profit = max(profit,prices[ptrB]-prices[ptrA]);
            }
        }
    return profit;
```

<hr>

# Best Solution - 1

## Idea

If we know max element at `ith` from end of list then we can easily solve the problem.

### Approach

- Create a vector and store the max elements till `ith` index from behind in it.
- Iterate from start to end-1 and find `diff = endMax[i+1] - prices[i]`.
- get maximum of this difference to get the answer.

| Time Complexity | Space Complexity : |
| :-------------: | :----------------: |
|     $O(n)$      |       $O(n)$       |

## Code

```
    int n = prices.size();
    vector<int> endMax(n);
    int profit = 0;
    endMax[n-1] = prices[n-1];
    for(int i = n-2 ; i >= 0 ; i--)
    {
        endMax[i] = max(endMax[i+1],prices[i]);
    }
    for(int i = 0 ; i < n-1 ; i++)
    {
        profit = max(profit,endMax[i+1]-prices[i]);
    }
    return profit;
```

# Best Solution - 2

## Idea

If we know min element at `ith` from start of list then we can easily solve the problem.

### Approach

- Iterate from start of list and at every index find `min_price` till that index.
- On each iteration find `profit_possible = prices[i]-min_price`
- Max of all the profits is the required answer

| Time Complexity | Space Complexity : |
| :-------------: | :----------------: |
|     $O(n)$      |       $O(1)$       |

## Code

```
    int n = prices.size();
    int profit = 0;
    int min_price = INT_MAX; // initializing with max Possible value
    for(int i = 0 ; i < n ; i++)
    {
        min_price = min(min_price,prices[i]);
        profit = max(profit,prices[i]-min_price);
    }
    return profit;
```
