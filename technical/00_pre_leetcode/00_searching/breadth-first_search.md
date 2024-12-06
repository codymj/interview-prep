# Breadth-first Search (BFS)

Used to traverse a graph structure from an initial node to all nodes in
increasing order based on the distance from the initial node.

Time complexity is
`O(V+E)` where `V` is the number of vertices and `E` is the number of edges.

Space complexity is `O(V)`.

Two ways to implement DFS:

1. Iteratively with an adjacency list
2. Iteratively with graph nodes

## Iteratively with an adjacency list

```c++
std::vector<std::vector<int>> graph;
std::vector<bool> visited;
std::queue<int> queue;

void bfs(int node) {
    // Initialize queue.
    visited[node] = true;
    queue.push(node);

    // Process queue until no nodes remain.
    while (!queue.empty()) {
        // Process current node in queue.
        int current = queue.front(); queue.pop();
        std::cout << current << std::endl;

        // Add all unvisited neighbors of current node to queue.
        for (auto neighbor : graph[current]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                queue.push(neighbor);
            }
        }
    }
}
```

## Iteratively with graph nodes

```c++
struct Node {
    int value;
    std::vector<Node*> neighbors;
};
std::unordered_set<Node*> visited;
std::queue<Node*> queue;

void bfs(Node* node) {
    // Initialize queue.
    queue.push(node);
    visited.insert(node);

    // Process queue until no nodes remain.
    while (!queue.empty()) {
        // Process current node in queue.
        Node* current = queue.front(); queue.pop();
        std::cout << current->value << std::endl;

        // Add all unvisited neighbors of current node to queue.
        for (Node* neighbor : current->neighbors) {
            if (!visited.count(neighbor)) {
                visisted.insert(neighbor);
                queue.push(neighbor);
            }
        }
    }
}
```
