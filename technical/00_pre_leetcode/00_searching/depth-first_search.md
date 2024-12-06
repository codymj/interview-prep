# Depth-first Search (DFS)

Used to traverse a graph structure from an initial node to all nodes that are
reachable from the starting node using graph edges.

Time complexity is `O(V+E)` where `V` is the number of vertices and `E` is the
number of edges.

Space complexity is `O(V)`.

Four ways to implement DFS:

1. Recursively with an adjacency list
2. Iteratively with an adjacency list
3. Recursively with graph nodes
4. Iteratively with graph nodes

## Recursively with an adjacency list

```c++
std::vector<std::vector<int>> graph;
std::vector<bool> visited;

void dfs(int node) {
    // If we've already visited this node, return.
    if (visited[node]) {
        return;
    }

    // Process this node.
    visited[node] = true;
    std::cout << node << std::endl;

    // Add all neighbors of this node to DFS call stack.
    for (auto neighbor : graph[node]) {
        dfs(neighbor);
    }
}
```

## Iteratively with an adjacency list

```c++
std::vector<std::vector<int>> graph;
std::vector<bool> visited;
std::stack<int> stack;

void dfs(int node)
{
    // Initialize stack.
    stack.push(node);

    // Process stack until no nodes remain.
    while (!stack.empty()) {
        // Process current node in stack.
        int current = stack.top(); stack.pop();
        if (!visited[current]) {
            visited[current] = true;
            std::cout << current << std::endl;

            // Add all unvisited neighbors of current node to stack.
            for (int neighbor : graph[current]) {
                if (!visited[neighbor]) {
                    stack.push(neighbor);
                }
            }
        }
    }
}
```

## Recursively with graph nodes

```c++
struct Node {
    int value;
    std::vector<Node*> neighbors;
};
std::unordered_set<Node*> visited;

void dfs(Node* node) {
    // If this node is null or visited, return.
    if (!node || visited.count(node)) {
        return;
    }

    // Process this node.
    visited.insert(node);
    std::cout << node->value << std::endl;

    // Add all neighbors of this node to DFS call stack.
    for (Node* neighbor : node->neighbors) {
        dfs(neighbor);
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
std::stack<Node*> stack;

void dfs(Node* node) {
    // Initialize stack.
    if (start) {
        stack.push(start);
    }

    // Process stack until no nodes remain.
    while (!stack.empty()) {
        // Process current node in stack.
        Node* current = stack.top(); stack.pop();
        if (!visited.count(current)) {
            visited.insert(node);
            std::cout << node->value << std::endl;

            // Add all unvisited neighbors of current node to stack.
            for (Node* neighbor : current->neighbors) {
                if (!visited.count(neighbor)) {
                    stack.push(neighbor);
                }
            }
        }
    }
}
```
