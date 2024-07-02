# Pre-LeetCode

This is a list of topics one should master _before_ attempting to drill LeetCode problems. Trying to solve LeetCode problems without these tools is akin to building a car without any tools — a waste of time. You will end up trying to memorize solutions rather than memorizing the tools required to derive the solutions; and it is much easier to memorize the tools.

Once the tools are mastered, the solutions become much more obvious, though still require practice of course.

This is the list that I used, but it is not exhaustive by any means. I consider it the bare minimum to solve LeetCode easy and medium problems confortably. It is also going to

## Containers

This may seem like a lot of containers, but the majority of them have similar interfaces. Know how to use them, their iterators, and be able to discuss their tradeoffs.

### Sequential Containers

- std::array
- std::vector
- std::queue
- std::priority_queue
- std::deque
- std::list
- std::stack
- std::string
- std::pair
- std::tuple

### Associative Containers

- std::set
- std::unordered_set
- std::multiset
- std::unordered_multiset
- std::map
- std::unordered_map
- std::multimap
- std::unordered_multimap

### Graphs and Trees

- adjacency list (`std::vector<int> adj[N];`)
- weighted adjacency list (`std::vector<std::pair<int,int>> adj[N];`)
- adjacency matrix (`int adj[N][N];`)
- edge list (`std::vector<std::pair<int,int>> edges;`)
- weighted edge list (`std::vector<std::tuple<int,int,int>> edges;`)

## Algorithms and Techniques

These are the bare, essential algorithms and techniques to master.

- binary search
- backtracking
- dynamic programming
- bit manipulation
- breadth-first search
- depth-first search
- pre-order traversal
- in-order traversal
- post-order traversal
- dijkstra's algorithm
