# LucyDS

**LucyDS** is a pure-Lucy data-structures and algorithms package for **Lucy 2.0.7**.

It provides linked lists, stacks, queues, hash tables, trees, heaps, tries,
graphs, disjoint sets, searching, and sorting algorithms.

## Requirements

- Lucy **2.0.7**
- No native extension or third-party runtime dependency

## Project layout

```text
LucyDS/
├── lucy.toml
├── packages/
│   └── lucyds/
│       ├── lucy.toml
│       └── src/
│           ├── init.lucy
│           ├── linked_list.lucy
│           ├── doubly_linked_list.lucy
│           ├── stack.lucy
│           ├── queue.lucy
│           ├── deque.lucy
│           ├── hash_table.lucy
│           ├── binary_search_tree.lucy
│           ├── avl_tree.lucy
│           ├── binary_heap.lucy
│           ├── trie.lucy
│           ├── graph.lucy
│           ├── union_find.lucy
│           ├── searching.lucy
│           ├── sorting.lucy
│           └── graph_algorithms.lucy
├── tests/
├── examples/
└── docs/
```

The package entry point is `packages/lucyds/src/init.lucy`. It selectively
imports the public API from sibling source modules. The runtime resolves
those imports relative to the entry file.

## Run the tests

From the repository root:

```bash
lucy tests/test_lucyds.lucy
```

The test file covers normal operations, empty states, boundary cases, queue
compaction, hash-table resizing, tree deletion, graph traversal, and algorithms.

## Use LucyDS

```lucy
import lucyds

let values = lucyds.LinkedList.new()
values.append(10)
values.append(20)
values.prepend(5)

println values.to_array()

let stack = lucyds.Stack.new()
stack.push("first")
stack.push("second")
println stack.pop()

let sorted = lucyds.merge_sort([8, 3, 5, 1])
println sorted
```

## Public API

| Category | Public names |
|---|---|
| Lists | `LinkedList`, `DoublyLinkedList` (`DoublyLinked` alias) |
| Linear structures | `Stack`, `Queue`, `Deque` |
| Hashing | `HashTable` |
| Trees | `BinarySearchTree`, `AVLTree`, `BinaryHeap`, `Trie` |
| Graphs | `Graph`, `UnionFind` |
| Searching | `linear_search`, `binary_search`, `lower_bound` |
| Sorting | `bubble_sort`, `selection_sort`, `insertion_sort`, `merge_sort`, `quick_sort` |
| Graph algorithms | `breadth_first_search`, `depth_first_search`, `dijkstra` |

See [`docs/API.md`](docs/API.md) for methods, constraints, and algorithm behavior.

## Design notes and limitations

- `HashTable` accepts **string keys**, because Lucy maps and the package's
  portable key handling use string keys. Values may be any Lucy value.
- `Graph` vertex identifiers and `UnionFind` elements are strings.
- `Graph` edge weights and `BinaryHeap` values must support numeric ordering.
- `binary_search` and `lower_bound` require an already sorted array.
- `dijkstra` returns `nil` if it encounters a negative edge reachable from
  the start vertex. Use non-negative weights with Dijkstra.
- `BinaryHeap` is a min-heap.
- Duplicate values are ignored by `BinarySearchTree` and `AVLTree`.
- The hash table uses separate chaining and a portable polynomial hash.
  Characters outside its built-in ASCII alphabet remain supported, but may
  produce more collisions.
- `AVLTree` currently supports insertion, lookup, traversal, and height;
  deletion is not implemented.
- This release does not yet include a generic `Set`, priority comparator,
  or weighted shortest-path algorithms beyond Dijkstra.

## Package discovery

Lucy 2.0.7 discovers project-local packages when a source file is executed
inside a directory tree containing the root `lucy.toml`. The root project's
`packages/` directory is added to module lookup. The package is imported as:

```lucy
import lucyds
```

The package manifest is included at `packages/lucyds/lucy.toml`. As described
in the Lucy 2.0.7 package documentation, the runtime's package discovery
currently relies on the project tree and `src/init.lucy`; the manifest is
metadata, not a fully enforced package-manager schema.

## License

GPL-3.0-only. See [`LICENSE`](LICENSE).
