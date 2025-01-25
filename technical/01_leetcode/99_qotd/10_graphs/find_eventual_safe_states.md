# [802. Find Eventual Safe States](https://leetcode.com/problems/find-eventual-safe-states)

There is a directed graph of `n` nodes with each node labeled from `0` to
`n - 1`. The graph is represented by a 0-indexed 2D integer array `graph` where
`graph[i]` is an integer array of nodes adjacent to node `i`, meaning there is
an edge from node `i` to each node in `graph[i]`.

A node is a terminal node if there are no outgoing edges. A node is a safe node
if every possible path starting from that node leads to a terminal node (or
another safe node).

Return an array containing all the safe nodes of the graph. The answer should be
sorted in ascending order.

Constraints:

* `n == graph.length`
* `1 <= n <= 10^4`
* `0 <= graph[i].length <= n`
* `0 <= graph[i][j] <= n - 1`
* `graph[i]` is sorted in a strictly increasing order.
* The graph may contain self-loops.
* The number of edges in the graph will be in the range `[1, 4 * 10^4]`.

## Solution

```c++
class Solution {
public:
    std::vector<int> eventualSafeNodes(std::vector<std::vector<int>>& graph) {
        int const N = graph.size();

        std::vector<bool> visited(N, 0);
        std::vector<bool> isTerminal(N, 0);

        // Function checks for cycles and if a cycle is not detected, the node
        // is marked true in isTerminal.
        std::function<bool(int const node)> isSafe = [&](int const node) -> bool {
            // Node in this path has been checked, return terminality.
            if (visited[node]) {
                return isTerminal[node];
            }

            // DFS for each edge (nodes connected to this node).
            visited[node] = true;
            for (int edge : graph[node]) {
                if (!isSafe(edge)) {
                    return false;
                }
            }

            // Reaching here indicates this node is a terminal node.
            isTerminal[node] = true;

            return true;
        };

        // Iterate over nodes to check safety.
        for (int node=0; node<N; ++node) {
            if (!visited[node]) {
                isSafe(node);
            }
        }

        // Iterate over nodes to check terminality.
        std::vector<int> ans{};
        for (int node=0; node<N; ++node) {
            if (isTerminal[node]) {
                ans.push_back(node);
            }
        }

        return ans;
    }
};
```

## Analysis

Time complexity is `O(V+E)` where `V` are vertices of the graph and `E` are
edges.

Space complexity is `O(V)` for the `visited` and `isTerminal` arrays and also
`O(V)` worst-case for the DFS call stack, resulting in `O(V)`.
