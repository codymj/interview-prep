# Post-Order Traversal

Post-order traversal is a depth-first tree traversal method where nodes are
visited in the following order:

1. Left (traverse the left subtree).
2. Right (traverse the right subtree).
3. Root (visit the current node).

It is commonly used for operations like deleting a tree or evaluating
expressions in an expression tree and can be recursive or iterative.

## Recursive

```c++
struct Node {
    int value;
    Node* left;
    Node* right;
};

void preOrder(Node* root) {
    if (!root) {
        return;
    }

    // Traverse left, traverse right, process current.
    preOrder(root->left);
    preOrder(root->right);
    std::cout << node->value << std::endl;
}
```

## Iterative

```c++
struct Node {
    int value;
    Node* left;
    Node* right;
};
std::stack<Node*> stack;

void postOrder(Node* root) {
    if (!root) {
        return;
    }
    Node* last = nullptr;
    Node* current = root;

    while (current || !stack.empty()) {
        // Push nodes onto stack while traversing to the leftmost node.
        if (current) {
            stack.push(current);
            current = current->left;
        } else {
            // Traverse the right subtree.
            Node* node = stack.top();
            if (node->right && node->right != last) {
                current = node->right;
            }

            // Process current node, set as the last visited node.
            else {
                std::cout << current->value << std::endl;
                stack.pop();
                last = node;
            }
        }
    }
}
```
