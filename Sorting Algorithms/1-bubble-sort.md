
# Bubble Sort

## Code

### Python Solution

````python

def bubble_sort(arr):
    for i in range(len(arr)):
        swapped = False
        for j in range(1, len(arr)-i-1):
            if arr[j-1] > arr[j]:
                arr[j], arr[j-1] = arr[j-1], arr[j]
                swapped = True
                
        if not swapped:
            break
            
    return arr

arr = [3, 5, 1, 7, 8, 9]
print(bubble_sort(arr))

````