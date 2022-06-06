# Brute Force Solution

Just add all elements from nums2 list to nums1 and sort the nums1.

| Time Complexity | Space Complexity : |
| :-------------: | :----------------: |
|   $O(nlogn)$    |       $O(1)$       |

## Code

```
    for(int i = m,j=0 ; i < m+n ; i++,j++)
    {
        nums1[i] = nums2[j];
    }
    sort(nums1.begin(), nums1.end());
```

<hr>

# Best Solution

## Idea

As Both list are sorted hence we can simply check on each iteration to add element in nums1 or not.

### Approach

- Take two pointers that point at start of each list.
- Start Iteration until both haven't reached the end `while(i < m && j < m)`.
- if element pointed by first pointer is smaller than element pointed by second pointer then it means there is no need to change that element and we can simply increment first pointer until we don't find an element smaller than first pointer element.
- If an Element is found such that `nums1[i] > nums2[j]` then swap them so that now nums1 contains the smaller element and not increament the first pointer by 1.
- Process repeats untill Whole array is not merged.

| Time Complexity | Space Complexity : |
| :-------------: | :----------------: |
|     $O(n)$      |       $O(1)$       |

## Code

```
    int_fast16_t i = 0 , j = 0;
        while(i < m && j < n)
        {
            if(nums1[i] <= nums2[0]) // no change needed simply move forward
                i++;
            else if(nums1[i] > nums2[0]) // swap the elements
            {
                swap(nums1[i],nums2[0]);
                for(int_fast16_t k = 1 ; k < n ; k++) // keep swapping until a bigger element is not found
                {
                    if(nums2[k] < nums2[k-1])
                        swap(nums2[k],nums2[k-1]);
                }
                i++;
            }
        }
        i = m,j = 0;
        while(i < m+n) // inserting the leftout elements
        {
            nums1[i] = nums2[j];
            i++,j++;
        }
```
