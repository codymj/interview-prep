# [295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream)

The median is the middle value in an ordered integer list. If the size of the
list is even, there is no middle value, and the median is the mean of the two
middle values.

    For example, for `arr = [2,3,4]`, the median is `3`.
    For example, for `arr = [2,3]`, the median is `(2 + 3) / 2 = 2.5`.

Implement the MedianFinder class:

* `MedianFinder()` initializes the `MedianFinder` object.
* `void addNum(int num)` adds the integer `num` from the data stream to the data
structure.
* `double findMedian()` returns the median of all elements so far. Answers
within `10^-5` of the actual answer will be accepted.

Constraints:

* `-10^5 <= num <= 10^5`
* There will be at least one element in the data structure before calling
`findMedian`.
* At most `5 * 10^4` calls will be made to `addNum` and `findMedian`.

## Solution

```c++
class MedianFinder {
private:
    std::priority_queue<int,std::vector<int>,std::greater<int>> m_min;
    std::priority_queue<int> m_max;
public:
    MedianFinder() {}

    void addNum(int num) {
        // Add num to first heap.
        m_max.push(num);

        // Rebalance the heaps.
        if (!m_min.empty() && !m_max.empty() && m_max.top() > m_min.top()) {
            m_min.push(m_max.top()); m_max.pop();
        }
        if (m_max.size() > m_min.size() + 1) {
            m_min.push(m_max.top()); m_max.pop();
        }
        if (m_min.size() > m_max.size() + 1) {
            m_max.push(m_min.top()); m_min.pop();
        }
    }

    double findMedian() {
        // If we have an odd number of elements, the median will be the extra
        // element in one of the heaps.
        // Otherwise, return the average of the two top elements.
        if (m_min.size() > m_max.size()) {
            return m_min.top();
        } else if (m_max.size() > m_min.size()) {
            return m_max.top();
        } else {
            return (m_min.top() + m_max.top()) * 0.5;
        }
    }
};

/*
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder* obj = new MedianFinder();
 * obj->addNum(num);
 * double param_2 = obj->findMedian();
 */
```

## Analysis

Time complexity for adding a number to the heaps and maintaining balance is
`O(logn)`. For finding the median, we just have to check the min or max heap so
it'll be `O(1)`.

Space complexity is `O(n)` due to having to store all of the nums between two
heaps.
