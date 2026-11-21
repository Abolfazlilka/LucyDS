# LucyDS API Reference

All names in this document are exported by `import lucyds`. `DoublyLinked` is also exported as a short alias for `DoublyLinkedList`.

## Lists

### `LinkedList`

Singly linked list with zero-based indexes.

- `append(value)`, `prepend(value)`: add an item; return the list.
- `insert(index, value)`: insert at an index; return `true` or `false`.
- `get(index)`: return a value or `nil` for an invalid index.
- `set(index, value)`: update an item; return `true` or `false`.
- `remove_at(index)`: remove and return the item, or `nil`.
- `remove(value)`: remove the first matching value; return a boolean.
- `contains(value)`, `index(value)`: search for a value.
- `size()`, `is_empty()`, `clear()`, `to_array()`, `reverse()`.

### `DoublyLinkedList`

Supports `append`, `prepend`, `insert`, `get`, `remove_at`, `remove`,
`contains`, `size`, `is_empty`, `clear`, `to_array`, and `to_array_reverse`.

## Linear structures

### `Stack`

`push`, `pop`, `peek`, `size`, `is_empty`, `clear`, `to_array`.

### `Queue`

FIFO queue: `enqueue`, `dequeue`, `peek`, `size`, `is_empty`, `clear`,
`to_array`. The backing array is periodically compacted after front removals.

### `Deque`

Double-ended queue: `push_front`, `push_back`, `pop_front`, `pop_back`,
`front`, `back`, `size`, `is_empty`, `clear`, `to_array`.

Empty removals/peeks return `nil`.

## Hashing

### `HashTable`

- `set(key, value)`: insert or replace; keys must be strings.
- `get(key)`: value or `nil`.
- `has(key)`, `delete(key)`.
- `keys()`, `values()`, `size()`, `is_empty()`, `load_factor()`, `clear()`.

Uses separate chaining and grows when the entry count exceeds three times the
bucket capacity. A missing key and a key mapped to `nil` both produce `nil`
from `get`; use `has` to distinguish them.

## Trees and trie

### `BinarySearchTree`

`insert`, `contains`, `remove`, `min`, `max`, `inorder`, `preorder`,
`postorder`, `size`, `is_empty`, `height`.

Duplicate values are not inserted. Values must support ordering.

### `AVLTree`

`insert`, `contains`, `inorder`, `size`, `height`, `is_empty`.

Duplicate values are not inserted. Self-balancing insertion is implemented;
deletion is not currently available.

### `BinaryHeap`

Min-heap: `push`, `peek`, `pop`, `size`, `is_empty`, `clear`, `to_array`.
Values must support numeric ordering.

### `Trie`

String prefix tree: `insert(word)`, `contains(word)`, `starts_with(prefix)`,
`size()`, `is_empty()`. Duplicate words are ignored.

## Graphs

### `Graph`

Create with `Graph.new()` for an undirected graph or
`Graph.new(true)` for a directed graph.

- `add_vertex(vertex)`, `has_vertex(vertex)`.
- `add_edge(from_vertex, to_vertex, weight = 1)`.
- `has_edge(from_vertex, to_vertex)`, `edge_weight(from_vertex, to_vertex)`.
- `neighbors(vertex)`, `vertices()`.
- `remove_edge(from_vertex, to_vertex)`, `remove_vertex(vertex)`.
- `vertex_count()`, `size()`, `edges_count()`, `is_directed()`.

Vertex identifiers are strings. Edge weights are numeric.

### Graph algorithms

- `breadth_first_search(graph, start)`: returns BFS visitation order.
- `depth_first_search(graph, start)`: returns DFS visitation order.
- `dijkstra(graph, start)`: returns a map of shortest distances. Unreachable
  vertices have `nil` distances. Returns `nil` if a negative edge is encountered
  while exploring vertices reachable from `start`.

### `UnionFind`

`add(value)`, `find(value)`, `union(first, second)`, `connected(first, second)`,
`components()`, `size()`. Elements must be strings.

## Searching

- `linear_search(items, target)`: index or `nil`; O(n).
- `binary_search(items, target)`: index or `nil`; O(log n), sorted input required.
- `lower_bound(items, target)`: first index whose value is not less than target;
  O(log n), sorted input required.

## Sorting

`bubble_sort`, `selection_sort`, `insertion_sort`, `merge_sort`, and
`quick_sort` return a **new sorted array** and do not mutate the input.
Values must support ordering.

| Algorithm | Average time | Extra space |
|---|---:|---:|
| Bubble sort | O(n²) | O(n) for copied result |
| Selection sort | O(n²) | O(n) for copied result |
| Insertion sort | O(n²) | O(n) for copied result |
| Merge sort | O(n log n) | O(n) plus recursion |
| Quick sort | O(n log n) | O(log n) average recursion, O(n) worst case |

The quick-sort implementation uses a middle element as pivot; worst-case
recursion depth can still be O(n).
