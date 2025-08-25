# ArrayQuestion-from-LeetCode
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.


# Idea (hashing)

As you scan the array once, keep a hash map from value → index.
For each number x = nums[i], the number you still need is y = target - x.

If y is already in the map, you’ve found the pair: [indexOf(y), i].

Otherwise, store x → i in the map and continue.

This is O(n) time and O(n) extra space.

## 🔎Dry Run Example

1. Input: nums = [2, 7, 11, 15], target = 9

   We’ll keep a map seen of {value: index}.

   i=0, x=2, need y=9-2=7
   seen doesn’t have 7 → put 2:0
   seen = { 2: 0 }

2. i=1, x=7, need y=9-7=2
   seen does have 2 at index 0 → return [0, 1] ✅
   
## Minimal pseudocode

seen = empty hash map
for i from 0 to n-1:
    x = nums[i]
    y = target - x
    if y in seen:
        return [seen[y], i]
    seen[x] = i
   
## C solution with a simple hash table (linear probing)
- Note :- Full code is available in the file Hashing_In_Array

## What the C hashmap is doing (step by step)

hash_int(x) maps any integer (even negatives) to a table index 0..TABLE_SIZE-1.

--->
    hm_put(m, key, value):
    
  1.  Compute h = hash_int(key).
    
  2.  If data[h] is empty, store (key, value) there.
    
  3.  If it’s occupied by a different key, move to h+1, then h+2, … (wrapping around) until an empty slot is found.

---> 
    hm_get(m, key, &out):
    
1.  Start at h = hash_int(key).
    
2.  If you see an empty slot, key isn’t in the map (stop).
    
3.  If the slot has our key, return the stored index.


Otherwise probe forward (h+1, h+2, …) until you find it or hit an empty slot.

Because we only insert each number once and look each complement up once, the average cost per operation is O(1), giving overall O(n) time and O(n) space.


## javaScript Hashing 
- Note :- Full code is available in the file JavaScript_Hashing

## Approach
- Use a hash map to store numbers while iterating.
- For each number `x`, compute `need = target - x`.
- If `need` is already in the hash map, return the indices.
- Otherwise, store `x` in the hash map.
- 
## 🔎Dry Run Example

Input:

- nums = [2,7,11,15], target = 9


- i=0, nums[0]=2, need=7
- seen = {} → 7 not found → store seen[2]=0.

- i=1, nums[1]=7, need=2
- seen = {2:0} → 2 is found → return [0,1].

- ✅ Output: [0,1].
