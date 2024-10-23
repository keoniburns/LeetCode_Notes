# Arrays

## 121. Best Time to Buy and Sell Stock

### Problem

You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

### Pseudocode and explanation

1. since were looking to maximize profit we need to track the minimum price and the maximum profit
2. iterate through the prices array and check two things

   - if the current price is lower than our current lowest price then update the min price

   - if not then check to see if the profit for the current price is greter than our max profit. If it is then update the max profit

3. return the max profit

```
function maxProfit(prices):
    if prices is empty or has only one element:
        return 0

    minPrice = infinity
    maxProfit = 0

    for price in prices:
        if price < minPrice:
            minPrice = price
        else:
            currentProfit = price - minPrice
            if currentProfit > maxProfit:
                maxProfit = currentProfit

    return maxProfit
```

## 1. Two Sum

### Problem

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

### Pseudocode and explanation

1. create a hash map to store the number and its index
2. iterate through the array and check if the complement of the current number (target - current number) exists in the hash map
3. if it does, return the indices of the current number and its complement
4. if not, add the current number and its index to the hash map
5. if no solution is found, return an empty array

```
function twoSum(nums, target):
    numToIndex = {}

    for i, num in enumerate(nums):
        complement = target - num
        if complement in numToIndex:
            return [numToIndex[complement], i]
        numToIndex[num] = i

    return []
```

## 11. Container With Most Water

### Problem

You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

### Pseudocode and explanation

1. initialize two pointers, left and right, to the start and end of the array
2. initialize a variable to store the maximum area
3. while the left pointer is less than the right pointer, calculate the area between the two pointers and update the maximum area if the current area is greater
4. move the pointer that points to the shorter line inward
5. return the maximum area

```
function maxArea(height):
    left = 0
    right = len(height) - 1
    maxArea = 0

    while left < right:
        currentArea = min(height[left], height[right]) * (right - left)
        maxArea = max(maxArea, currentArea)
        if height[left] < height[right]:
            left += 1
        else:
            right -= 1
    return maxArea
```
