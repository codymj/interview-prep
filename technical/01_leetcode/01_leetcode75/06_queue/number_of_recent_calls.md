# [933. Number of Recent Calls](https://leetcode.com/problems/number-of-recent-calls)

You have a `RecentCounter` class which counts the number of recent requests within a certain time frame.

Implement the `RecentCounter` class:

* `RecentCounter()` Initializes the counter with zero recent requests.
* `int ping(int t)` Adds a new request at time `t`, where `t` represents some
time in milliseconds, and returns the number of requests that has happened in
the past `3000` milliseconds (including the new request). Specifically, return
the number of requests that have happened in the inclusive range
`[t - 3000, t]`.

It is guaranteed that every call to ping uses a strictly larger value of `t`
than the previous call.

Constraints:

* `1 <= t <= 10^9`
* Each test case will call ping with strictly increasing values of `t`.
* At most `10^4` calls will be made to ping.

## Solution

```c++
class RecentCounter {
    std::vector<int> m_calls{};
    int start;

public:
    RecentCounter() : start(0) {}

    int ping(int t) {
        m_calls.push_back(t);

        while (m_calls[start] < t - 3000) {
            start++;
        }

        return m_calls.size() - start;
    }
};

/**
 * Your RecentCounter object will be instantiated and called as such:
 * RecentCounter* obj = new RecentCounter();
 * int param_1 = obj->ping(t);
 */
```

## Analysis

Time complexity is `O(1)` since we're appending to the end of the vector and
iterating over a fixed window of times.

Space complexity is `O(1)` to store all of the times.
