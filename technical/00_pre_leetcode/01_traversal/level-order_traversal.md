# Level-Order Traversal

Level-order traversal visits nodes level by level, starting from the root, then
moving to all nodes at the next level, and so on. It uses a queue to process
nodes in breadth-first order.

This traversal is commonly used for tasks like finding the shortest path in an unweighted tree.

```c++
struct Node {
    int value;
    Node* left;
    Node* right;
};
std::queue<Node*> queue;

void levelOrder(Node* root) {
    if (!root) {
        return;
    }
    queue.push(root);

    while (!queue.empty()) {
        Node* current = queue.front(); queue.pop();

        // Process node.
        std::cout << current->value << std::endl;

        // Add both children to the queue.
        if (current->left) {
            queue.push(current->left);
        }
        if (current->right) {
            queue.push(current->right);
        }
    }
}
```
