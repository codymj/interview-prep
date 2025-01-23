# [133. Clone Graph](https://leetcode.com/problems/clone-graph)

Given a reference of a node in a connected undirected graph.

Return a deep copy (clone) of the graph.

Constraints:

* The number of nodes in the graph is in the range `[0, 100]`.
* `1 <= Node.val <= 100`
* `Node.val` is unique for each node.
* There are no repeated edges and no self-loops in the graph.
* The Graph is connected and all nodes can be visited starting from the given
node.

## Solution

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> neighbors;
    Node() {
        val = 0;
        neighbors = vector<Node*>();
    }
    Node(int _val) {
        val = _val;
        neighbors = vector<Node*>();
    }
    Node(int _val, vector<Node*> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
};
*/
class Solution {
public:
    Node* cloneGraph(Node* node) {
        if (!node) {
            return nullptr;
        }

        // Map given nodes to new nodes. Clone the root node.
        std::unordered_map<Node*, Node*> visited{};
        visited[node] = new Node(node->val);

        // DFS stack to traverse nodes.
        std::stack<Node*> stack{};
        stack.push(node);
        while (!stack.empty()) {
            // Get node on stack and clone its neighbors.
            Node* current = stack.top(); stack.pop();
            for (Node* neighbor : current->neighbors) {
                // Add neighbor on to stack to clone it's neighbors.
                if (!visited.count(neighbor)) {
                    visited[neighbor] = new Node(neighbor->val);
                    stack.push(neighbor);
                }

                // Add the cloned neighbor to cloned current's neighbors.
                visited[current]->neighbors.push_back(visited[neighbor]);
            }
        }

        return visited[node];
    }
};
```

## Analysis

Time complexity is `O(V+E)` where `V` is the number of vertices (nodes) and `E`
is the number of edges (neighbors of each node).

Space complexity is `O(V)` where `V` is the number of cloned vertices (nodes)
stored in the `visited` map.
