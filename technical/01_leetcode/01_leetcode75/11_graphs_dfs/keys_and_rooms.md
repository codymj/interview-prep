# [841. Keys and Rooms](https://leetcode.com/problems/keys-and-rooms)

There are `n` rooms labeled from `0` to `n - 1` and all the rooms are locked
except for room `0`. Your goal is to visit all the rooms. However, you cannot
enter a locked room without having its key.

When you visit a room, you may find a set of distinct keys in it. Each key has a
number on it, denoting which room it unlocks, and you can take all of them with
you to unlock the other rooms.

Given an array rooms where `rooms[i]` is the set of keys that you can obtain if
you visited room `i`, return `true` if you can visit all the rooms, or `false`
otherwise.

Constraints:

* `n == rooms.length`
* `2 <= n <= 1000`
* `0 <= rooms[i].length <= 1000`
* `1 <= sum(rooms[i].length) <= 3000`
* `0 <= rooms[i][j] < n`
* All the values of `rooms[i]` are unique.

## Solution

```c++
class Solution {
public:
    bool canVisitAllRooms(std::vector<std::vector<int>>& rooms) {
        int const N = rooms.size();

        // Keep track of visited rooms.
        std::vector<bool> visited(N, false);

        // BFS queue.
        std::queue<int> queue{};
        queue.push(0);

        // Visit rooms until we run out of keys.
        int current{};
        while (!queue.empty()) {
            // Get next room to visit.
            current = queue.front(); queue.pop();
            visited[current] = true;

            // Grab keys in the current room and add to queue.
            for (int room : rooms[current]) {
                if (!visited[room]) {
                    queue.push(room);
                }
            }
        }

        return !std::any_of(visited.begin(), visited.end(), [](bool b) { return !b; });
    }
};
```

## Analysis

Time complexity is `O(n+k)` where `n` is number of rooms and `k` is number of
keys. Even though we do not visit each room more than once, we still have to
process every key from each room.

Space complexity is `O(n)` worst-case if all rooms are added to the queue, as
well as keeping track of which rooms were visited.
