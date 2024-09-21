# Computer Science Fundamentals

## Data Structures

### Arrays and Linked Lists
- **Arrays**: Contiguous memory blocks storing elements of the same type. They offer constant-time access to elements by index but have a fixed size.
  - Example: `int[] numbers = {1, 2, 3, 4, 5};`
  - Use cases: When you need fast random access and know the size in advance.

- **Linked Lists**: Sequences of nodes, each containing data and a reference to the next node. They allow for dynamic size but have linear-time access to elements.
  - Example: `class Node { int data; Node next; }`
  - Use cases: When you need frequent insertions/deletions and don't need random access.

### Stacks and Queues
- **Stacks**: Last-In-First-Out (LIFO) data structures. Elements are added and removed from the same end.
  - Operations: push (add), pop (remove), peek (view top)
  - Example: Function call stack, undo functionality in applications

- **Queues**: First-In-First-Out (FIFO) data structures. Elements are added at one end and removed from the other.
  - Operations: enqueue (add), dequeue (remove), peek (view front)
  - Example: Print job scheduling, breadth-first search algorithm

### Trees and Graphs
- **Trees**: Hierarchical data structures with a root node and child nodes.
  - Types: Binary trees, AVL trees, Red-Black trees, B-trees
  - Use cases: File systems, organization charts, DOM in web browsers

- **Graphs**: Collections of nodes (vertices) connected by edges.
  - Types: Directed/Undirected, Weighted/Unweighted, Cyclic/Acyclic
  - Use cases: Social networks, map applications, recommendation systems

### Hash Tables
- Data structures that store key-value pairs and use a hash function to compute an index for fast data retrieval.
- Provide average-case constant time complexity for insert, delete, and lookup operations.
- Example: Dictionaries in Python, HashMap in Java
- Use cases: Caching, database indexing, symbol tables in compilers

### Heaps
- Specialized tree-based data structures satisfying the heap property.
- Types: Min-heap (parent smaller than children), Max-heap (parent larger than children)
- Used for implementing priority queues and in algorithms like heapsort.
- Operations: insert, extract-min/max, peek
- Use cases: Task scheduling, finding the kth smallest/largest element

## Algorithms

### Sorting Algorithms
- **Quicksort**:
  - Divide-and-conquer algorithm
  - Average time complexity: O(n log n)
  - Chooses a pivot, partitions the array, and recursively sorts subarrays

- **Mergesort**:
  - Divide-and-conquer algorithm
  - Time complexity: O(n log n)
  - Divides the array, recursively sorts, and merges sorted subarrays

### Searching Algorithms
- **Binary Search**:
  - Efficient algorithm for searching sorted arrays
  - Time complexity: O(log n)
  - Repeatedly divides the search interval in half

### Graph Algorithms
- **Breadth-First Search (BFS)**:
  - Explores all vertices of a graph in breadth-first order
  - Uses a queue to keep track of vertices to visit
  - Time complexity: O(V + E) where V is the number of vertices and E is the number of edges

- **Depth-First Search (DFS)**:
  - Explores as far as possible along each branch before backtracking
  - Uses a stack (or recursion) to keep track of vertices to visit
  - Time complexity: O(V + E)

### Dynamic Programming
- Problem-solving technique that solves complex problems by breaking them down into simpler subproblems
- Stores results of subproblems to avoid redundant computations
- Examples: Fibonacci sequence, Longest Common Subsequence, Knapsack problem

### Recursion
- Programming technique where a function calls itself to solve a problem
- Consists of a base case and a recursive case
- Examples: Factorial calculation, tree traversal, fractal generation

## Time and Space Complexity

### Big O Notation
- Describes the upper bound of the growth rate of an algorithm's time or space requirements
- Common complexities:
  - O(1): Constant time
  - O(log n): Logarithmic time
  - O(n): Linear time
  - O(n log n): Linearithmic time
  - O(n^2): Quadratic time
  - O(2^n): Exponential time

### Analyzing Algorithm Efficiency
- Focuses on how the runtime or space requirements grow as input size increases
- Considers worst-case, average-case, and best-case scenarios
- Helps in comparing algorithms and choosing the most efficient one for a given problem

### Trade-offs Between Time and Space Complexity
- Often, reducing time complexity comes at the cost of increased space complexity (and vice versa)
- Example: Memoization in dynamic programming trades space for time
- Choosing the right balance depends on the specific requirements of the application

## Basic Networking Concepts

### HTTP/HTTPS Protocols
- **HTTP (Hypertext Transfer Protocol)**:
  - Application-layer protocol for transmitting hypermedia documents
  - Uses a client-server model
  - Stateless protocol

- **HTTPS (HTTP Secure)**:
  - Encrypted version of HTTP
  - Uses SSL/TLS for secure communication
  - Provides authentication, data integrity, and confidentiality

### RESTful API Design Principles
- **RE**presentational **S**tate **T**ransfer
- Architectural style for designing networked applications
- Key principles:
  - Client-server architecture
  - Statelessness
  - Cacheability
  - Uniform interface
  - Layered system

### WebSockets
- Protocol providing full-duplex communication channels over a single TCP connection
- Enables real-time, bidirectional communication between clients and servers
- Use cases: Chat applications, live updates, online gaming

### CORS (Cross-Origin Resource Sharing)
- Security mechanism that allows a web page from one domain to request resources from another domain
- Relaxes the Same-Origin Policy
- Controlled through HTTP headers
- Important for building web applications that consume APIs from different domains

### API Authentication and Security
- Ensures that only authorized users or applications can access the API
- Common authentication methods:
  - API Keys
  - OAuth 2.0
  - JSON Web Tokens (JWT)
- Best practices:
  - Use HTTPS
  - Implement rate limiting
  - Validate and sanitize input
  - Use appropriate authorization mechanisms
