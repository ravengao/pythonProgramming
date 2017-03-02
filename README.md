Common Programming questions solution (with python)

- These are my own solutions, still on update and refinement :)

# Intersection:
common elements in 2 arrays with repeted elements


```python
def intersection(nums1, nums2):
    intersec = []
    for x in nums1:
        if x in nums2:
            intersec.append(x)
            nums2.remove(x)
    return intersec

#refined version: calculate # of each number 
def intersection2(nums1, nums2):
    numscounter1 = [0]*10#
    numscounter2 = [0]*10#
    intersec = []
    finalIntersect = []
    for x in nums1:
        numscounter1[x] += 1
    for y in nums2:
        numscounter2[y] += 1
    for i in range(10):
        if(numscounter1[i] > numscounter2[i]):
            intersec.append(numscounter2[i])
        else:
            intersec.append(numscounter1[i]);
    
    for i in intersec:
        if(i > 0):
            for j in range(i):finalIntersect.append(i)
    return finalIntersect

#refined version: hash table(dict)
def intersection3(nums1, nums2):
    numscounter = {}#
    intersec = []
    for x in nums1:
        if x in numscounter:
            numscounter[x] += 1
        else:
            numscounter[x] = 1
    for y in nums2:
        if numscounter[y] > 0:
            intersec.append(y)
            numscounter[y] = numscounter[y] - 1
    return intersec

        
nums1 = [1, 2, 1,2,9]
nums2 = [2,2,9]

%timeit intersection(nums1, nums2)
%timeit intersection2(nums1, nums2)
%timeit intersection3(nums1, nums2)
```

    The slowest run took 11.95 times longer than the fastest. This could mean that an intermediate result is being cached.
    1000000 loops, best of 3: 437 ns per loop
    100000 loops, best of 3: 5.16 µs per loop
    1000000 loops, best of 3: 1.05 µs per loop



# Two Sums: sorted array
if sorted, think about using start and end to solve problems


```python
def twoSum(numbers, target):
    index1=0
    index2=len(numbers)-1#index1 < index2
    while(index1<index2):
        numSum = numbers[index1] + numbers[index2]
        if numSum == target:
            return index1+1,index2+1
        elif numSum < target:
            index1 += 1
        elif numSum > target:
            index2 -= 1
    
    
twoSum(numbers=[3,2,1], target=0)
```
# Third Max problem (K-th max)
1. mergesort
```python
#normal method: go through each element
def thirdMax(nums):
    seqDict = {1:None,2:None,3:None}
    for x in nums:
        if (seqDict[1] == None) or (x > seqDict[1]):
            seqDict[3] = seqDict[2]
            seqDict[2] = seqDict[1]
            seqDict[1] = x
            continue
        if (seqDict[2] == None) or (x > seqDict[2]) & (x < seqDict[1]):
            if x!=seqDict[1]:
                seqDict[3] = seqDict[2]
                seqDict[2] = x
                continue
        if (seqDict[3] == None) or (x > seqDict[3]) & (x < seqDict[2]):
            if (x!=seqDict[2]) & (x!=seqDict[1]):
                seqDict[3] = x
                continue
    print(seqDict)
    if seqDict[3] == None:
        return seqDict[1]
    else:
        return seqDict[3]
thirdMax([2,2,2])  


#use mergesort of python: sort()
#Time Complexity: O(nlogn)
def findKthLargest(nums, k):
    nums.sort(reverse=True)
    print(nums)
    return nums[k-1]
       
findKthLargest([1,2,3,3,4,5], 4)
```
2. quicksort (still working on it)

# Search index to insert a number in an array
```python
#pay attention to different conditions
def searchInsert(nums, target):
    start=0
    end=len(nums)-1
    while(start<=end):
        if nums[start] == target:
            return start
        if nums[end] == target:
            return end
            
        if target > nums[end]:
            return end+1
        if target < nums[start]:
            return start
            
        if start + 1 == end:
            return end
            
        if target > nums[start]:
            start += 1
        if target < nums[end]:
            end -= 1
    print(nums)

searchInsert([1,3,6,8],5)
```
# Rotate an array
use reverse*3
```python
def rotate(nums, k):
    n = len(nums)
    arr= [0]*n
    for i in range(n):
        arr[(i+k)%n] = nums[i]
    for i in range(n):
        nums[i] = arr[i]
    print(arr)

def rotate1(nums,k):
    n=len(nums)
    reverse(nums,0,n-1)
    reverse(nums,0,k-1)
    reverse(nums,k,n-1)
    
def reverse(arr, start, end):
    while start < end:
        temp = arr[end]
        arr[end] = arr[start]
        arr[start] = temp
        start += 1
        end -= 1
    print(arr)
    
rotate1([1,2,3,4,5,6,7],3)
```
