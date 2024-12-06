# Binary Search

Used to find an element within a sorted array in `O(logn)` time.

```c++
// Initialize the bounds.
int a=0, b=array.size()-1;
while (a<=b) {
    // k is mid-point between our bounds (avoid potential overflow).
    int k = a+(b-a)/2;
    if (array[k] == x) {
        // x is found
    }

    // If we did not find x, shift one bound based on current element.
    if (array[k] < x) {
        a = k+1;
    } else {
        b = k-1;
    }
}
```