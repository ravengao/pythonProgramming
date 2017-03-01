Common Programming questions solution (with python)

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
