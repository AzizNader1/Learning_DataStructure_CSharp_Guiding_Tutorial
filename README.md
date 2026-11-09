# Data Structures in C# — From Absolute Beginner to Mastery

> A complete, progressive, practical guide to understanding, choosing, implementing, testing, and applying data structures in C#.

Data structures are the ways we organize information so that algorithms can use it effectively. This guide begins with absolute fundamentals and gradually builds toward advanced structures, performance trade-offs, generic implementations, custom data structures, and a complete application project.

The main project is a **Data Structure Lab** that reads event data and uses arrays, lists, dictionaries, sets, queues, stacks, heaps, and trees to answer practical questions efficiently.

---

## Table of Contents

1. [How to Use This Guide](#1-how-to-use-this-guide)
2. [Chapter 1 — What a Data Structure Is](#2-chapter-1--what-a-data-structure-is)
3. [Chapter 2 — A Short History](#3-chapter-2--a-short-history)
4. [Chapter 3 — Why Data Structures Matter](#4-chapter-3--why-data-structures-matter)
5. [Chapter 4 — C# and .NET Foundations](#5-chapter-4--c-and-net-foundations)
6. [Chapter 5 — Analyze the Data Before Choosing a Structure](#6-chapter-5--analyze-the-data-before-choosing-a-structure)
7. [Chapter 6 — Memory, References, and Generics](#7-chapter-6--memory-references-and-generics)
8. [Chapter 7 — Arrays and Spans](#8-chapter-7--arrays-and-spans)
9. [Chapter 8 — Lists and Dynamic Arrays](#9-chapter-8--lists-and-dynamic-arrays)
10. [Chapter 9 — Dictionaries and Hash Tables](#10-chapter-9--dictionaries-and-hash-tables)
11. [Chapter 10 — Sets and Uniqueness](#11-chapter-10--sets-and-uniqueness)
12. [Chapter 11 — Stacks and Queues](#12-chapter-11--stacks-and-queues)
13. [Chapter 12 — Linked Lists](#13-chapter-12--linked-lists)
14. [Chapter 13 — Priority Queues and Heaps](#14-chapter-13--priority-queues-and-heaps)
15. [Chapter 14 — Trees and Binary Search Trees](#15-chapter-14--trees-and-binary-search-trees)
16. [Chapter 15 — Balanced Trees and Ordered Data](#16-chapter-15--balanced-trees-and-ordered-data)
17. [Chapter 16 — Graphs](#17-chapter-16--graphs)
18. [Chapter 17 — Immutable and Specialized Structures](#18-chapter-17--immutable-and-specialized-structures)
19. [Chapter 18 — Data Structures for Data Analysis](#19-chapter-18--data-structures-for-data-analysis)
20. [Chapter 19 — Build the Data Structure Lab](#20-chapter-19--build-the-data-structure-lab)
21. [Chapter 20 — Testing and Benchmarking](#21-chapter-20--testing-and-benchmarking)
22. [Chapter 21 — Architecture, Concurrency, and Production](#22-chapter-21--architecture-concurrency-and-production)
23. [Chapter 22 — Mastery Roadmap](#23-chapter-22--mastery-roadmap)
24. [Appendix A — Complexity Reference](#appendix-a--complexity-reference)
25. [Appendix B — Vocabulary](#appendix-b--vocabulary)
26. [Appendix C — Practice Challenges](#appendix-c--practice-challenges)

---

# 1. How to Use This Guide

## 1.1 The learning method

For every structure:

1. Understand what problem it solves.
2. Draw a small example on paper.
3. Learn its core operations.
4. Learn the cost of each operation.
5. Implement a minimal version.
6. Compare it with a standard .NET collection.
7. Test empty, one-item, duplicate, and large cases.
8. Use it in a small application.

## 1.2 What mastery means

You do not need to memorize every collection type. Mastery means you can:

- describe how a structure stores data;
- identify its invariants;
- choose it based on required operations;
- state expected time and memory costs;
- implement it using clear C#;
- recognize invalid states;
- test boundary cases;
- explain its trade-offs;
- replace it when the workload changes.

## 1.3 The central question

Do not ask:

> “Which data structure is famous?”

Ask:

> “Which operations must be fast, and what guarantees do I need?”

---

# 2. Chapter 1 — What a Data Structure Is

## 2.1 Definition

A **data structure** is a systematic way to organize, store, and access data.

Examples:

- an array stores values in contiguous indexed positions;
- a list stores an ordered sequence that can grow;
- a dictionary maps keys to values;
- a queue processes items in arrival order;
- a tree represents hierarchy;
- a graph represents relationships.

## 2.2 Data structure versus data type

A **data type** describes what kind of value something is, such as `int`, `string`, or `bool`.

A **data structure** describes how one or more values are organized, such as `List<int>` or `Dictionary<string, decimal>`.

A class can be both a data type and an implementation of a data structure.

## 2.3 Data structure versus algorithm

A data structure organizes data. An algorithm performs operations on that organization.

For example:

- `Dictionary<int, Customer>` is a structure;
- looking up a customer by ID is an operation;
- hashing is part of the algorithm used by the dictionary.

A strong solution chooses the structure and algorithm together.

## 2.4 Abstract data type

An **abstract data type** describes behavior without requiring a particular implementation.

A stack promises:

- add an item to the top;
- remove the most recently added item;
- inspect the top item.

It may be implemented with an array or a linked list. The user of the stack should depend on its behavior, not its internal details.

## 2.5 Interface and implementation

An interface describes what can be done:

```csharp
public interface IStack<T>
{
    int Count { get; }
    void Push(T value);
    T Pop();
    T Peek();
}
```

An implementation decides how it is done.

## 2.6 Operations to identify

For every data collection, ask whether you need:

- access by index;
- search by value;
- lookup by key;
- insertion;
- deletion;
- uniqueness;
- ordering;
- minimum or maximum retrieval;
- traversal;
- range queries;
- relationship queries;
- concurrency;
- immutability.

These needs determine the best structure.

---

# 3. Chapter 2 — A Short History

## 3.1 Early organization of information

People have always organized information: lists, tables, maps, family trees, ledgers, and filing systems are all physical data structures.

The core questions were already present:

- How quickly can an item be found?
- How much space does organization require?
- How can new records be inserted?
- How can duplicates be prevented?

## 3.2 Mathematical and mechanical structures

Mathematical procedures introduced sequences, tables, sets, and relationships. Mechanical calculators made it useful to represent information in machine-readable arrangements.

As computers developed, programmers created structures suited to memory and processor behavior:

- contiguous arrays;
- linked nodes;
- stacks for procedure calls;
- queues for scheduled work;
- trees for ordered search;
- graphs for networks.

## 3.3 Modern library collections

Modern languages package proven data structures into standard libraries. C# and .NET provide collections such as:

- `Array`;
- `List<T>`;
- `Dictionary<TKey, TValue>`;
- `HashSet<T>`;
- `Stack<T>`;
- `Queue<T>`;
- `PriorityQueue<TElement, TPriority>`;
- `LinkedList<T>`;
- immutable and concurrent collections.

Knowing the concepts allows you to choose these libraries intelligently and build custom structures when necessary.

---

# 4. Chapter 3 — Why Data Structures Matter

## 4.1 Same data, different performance

Suppose you need to find a customer by ID.

With a list, you may scan every customer: expected `O(n)` time.

With a dictionary keyed by ID, lookup is usually expected `O(1)` time.

The data is the same. The organization is different.

## 4.2 Correctness and invariants

Each structure has rules called **invariants**.

Examples:

- a stack removes the most recent item;
- a queue removes the oldest waiting item;
- a binary search tree maintains ordering;
- a heap keeps its priority relationship;
- a set contains no duplicates;
- a dictionary has at most one value for each key.

If an operation violates an invariant, the structure is broken even if the program compiles.

## 4.3 Memory and locality

An array stores elements close together in memory. This often improves cache behavior and indexed access.

A linked structure stores nodes in separate locations connected by references. It may make certain insertions easy but can be less cache-friendly.

Theoretical complexity matters, but real performance also depends on:

- allocations;
- memory locality;
- garbage collection;
- object size;
- branch behavior;
- synchronization;
- input distribution.

## 4.4 A practical decision example

Requirement:

> “Store every event, preserve insertion order, and frequently find events by user ID.”

A single structure may not be best for every operation. Use:

- `List<Event>` for ordered history;
- `Dictionary<int, List<Event>>` for lookup by user ID.

This is called an **index**: an additional structure that makes a query faster.

---

# 5. Chapter 4 — C# and .NET Foundations

## 5.1 Create a project

```bash
dotnet new console -n DataStructureJourney
cd DataStructureJourney
dotnet run
```

The .NET SDK builds and runs the C# project. The code in this guide uses modern C# syntax.

## 5.2 Generic types

A generic type works with a specified element type:

```csharp
List<int> numbers = new();
List<string> names = new();
```

`T` is commonly used as a placeholder for a type parameter:

```csharp
public sealed class Box<T>
{
    public Box(T value)
    {
        Value = value;
    }

    public T Value { get; }
}
```

`Box<int>` stores an integer; `Box<string>` stores a string.

## 5.3 Interfaces

Program to an interface when you care about behavior:

```csharp
IReadOnlyList<int> values = new List<int> { 1, 2, 3 };
```

The caller can use read-only list behavior without depending on the concrete implementation.

## 5.4 `IEnumerable<T>` and enumeration

`IEnumerable<T>` means a sequence can be traversed:

```csharp
static int CountItems<T>(IEnumerable<T> items)
{
    int count = 0;

    foreach (T item in items)
    {
        count++;
    }

    return count;
}
```

Be aware that enumerating a lazy sequence may execute work each time. Calling `ToList()` materializes the values.

---

# 6. Chapter 5 — Analyze the Data Before Choosing a Structure

## 6.1 Requirement table

Create an operation table before choosing:

| Operation | Frequency | Required speed |
|---|---:|---|
| append event | very high | fast |
| retrieve by index | low | not important |
| find by ID | very high | very fast |
| preserve order | required | yes |
| remove by ID | medium | reasonable |

This may suggest a list plus dictionary index rather than one collection.

## 6.2 Questions about the data

Ask:

- Is the size fixed or changing?
- Are duplicates allowed?
- Is order meaningful?
- Is sorted order required?
- Are keys unique?
- Will values be updated often?
- Must the structure be thread-safe?
- Can data be null?
- Is the collection read-only after creation?
- Does the data arrive as a stream?

## 6.3 Workload beats habit

A `List<T>` is a good default for many application collections, but not for every workload.

Examples:

- use `HashSet<T>` for membership and uniqueness;
- use `Dictionary<TKey, TValue>` for key lookup;
- use `Queue<T>` for first-in-first-out work;
- use `Stack<T>` for last-in-first-out work;
- use a priority queue for “next most urgent” work;
- use a tree for ordered hierarchical data;
- use a graph for arbitrary relationships.

## 6.4 Record the decision

A professional design note might say:

> We use a list for ordered event history and a dictionary index for lookup by user ID. The list preserves output order; the index avoids repeated full scans. The cost is additional memory and the need to update both structures consistently.

This explanation is more valuable than simply naming a collection.

---

# 7. Chapter 6 — Memory, References, and Generics

## 7.1 Value types and reference types

A value-type variable contains a value. A reference-type variable points to an object.

```csharp
int first = 10;
int second = first;
second = 20;
```

`first` remains `10`.

With a list:

```csharp
List<int> firstList = new() { 1, 2 };
List<int> secondList = firstList;
secondList.Add(3);
```

Both variables refer to the same list, so `firstList` also contains `3`.

## 7.2 Null references

A reference may be `null`, meaning no object is referenced:

```csharp
List<string>? names = null;
```

Use nullable reference annotations and validate before access.

## 7.3 Equality

Data structures often depend on equality. For custom objects, decide whether equality means:

- same object identity;
- same ID;
- same fields;
- same normalized value.

Dictionaries and sets rely on equality and hashing. Incorrect equality behavior can produce missing or duplicate-looking entries.

## 7.4 A generic node

```csharp
public sealed class Node<T>
{
    public Node(T value)
    {
        Value = value;
    }

    public T Value { get; }
    public Node<T>? Next { get; set; }
}
```

- `Node<T>` works for any element type.
- `T Value` stores the value.
- `Node<T>? Next` can reference another node or be null at the end.

---

# 8. Chapter 7 — Arrays and Spans

## 8.1 Arrays

An array has a fixed length and zero-based indexes:

```csharp
int[] scores = { 90, 75, 88 };
Console.WriteLine(scores[0]);
scores[1] = 80;
```

Operations:

- index access: `O(1)`;
- update by index: `O(1)`;
- search by value: `O(n)`;
- insert into the middle: requires shifting and is `O(n)`;
- length: `O(1)`.

## 8.2 Multidimensional arrays

```csharp
int[,] grid = new int[3, 3];
grid[1, 2] = 7;
```

Use them for rectangular data. For irregular rows, a jagged array may be clearer:

```csharp
int[][] rows =
{
    new[] { 1, 2 },
    new[] { 3, 4, 5 }
};
```

## 8.3 Array slicing

```csharp
int[] numbers = { 0, 1, 2, 3, 4 };
int[] middle = numbers[1..4];
```

The range `1..4` includes index 1 and excludes index 4.

## 8.4 `Span<T>` concept

`Span<T>` represents a window over contiguous memory without necessarily allocating a new array:

```csharp
static int Sum(Span<int> values)
{
    int total = 0;

    foreach (int value in values)
    {
        total += value;
    }

    return total;
}
```

Use spans when performance-sensitive code works with contiguous memory. They have restrictions, including not being usable across asynchronous boundaries in the same way ordinary collections are.

## 8.5 When arrays are best

Use arrays when:

- the length is known;
- indexed access is central;
- data is processed sequentially;
- low overhead matters;
- the structure should not grow.

---

# 9. Chapter 8 — Lists and Dynamic Arrays

## 9.1 `List<T>`

```csharp
List<string> names = new();
names.Add("Ari");
names.Add("Bo");
names.Insert(1, "Cy");
names.Remove("Bo");
```

A list uses an internal array and grows when capacity is exhausted.

## 9.2 Capacity and count

```csharp
List<int> values = new(capacity: 100);
Console.WriteLine(values.Count);
Console.WriteLine(values.Capacity);
```

- `Count` is the number of stored elements.
- `Capacity` is the number of elements the internal storage can hold before resizing.

Resizing may allocate a larger array and copy elements. Because capacity grows geometrically, appending is usually `O(1)` amortized.

## 9.3 Implement a simple dynamic array

```csharp
public sealed class DynamicArray<T>
{
    private T[] _items;

    public DynamicArray(int initialCapacity = 4)
    {
        if (initialCapacity <= 0)
        {
            throw new ArgumentOutOfRangeException(nameof(initialCapacity));
        }

        _items = new T[initialCapacity];
    }

    public int Count { get; private set; }

    public T this[int index]
    {
        get
        {
            CheckIndex(index);
            return _items[index];
        }
        set
        {
            CheckIndex(index);
            _items[index] = value;
        }
    }

    public void Add(T value)
    {
        if (Count == _items.Length)
        {
            Array.Resize(ref _items, _items.Length * 2);
        }

        _items[Count] = value;
        Count++;
    }

    private void CheckIndex(int index)
    {
        if (index < 0 || index >= Count)
        {
            throw new ArgumentOutOfRangeException(nameof(index));
        }
    }
}
```

Line-by-line concepts:

- `_items` is private storage.
- The constructor creates initial storage and rejects invalid capacity.
- `Count` tracks logical size separately from physical capacity.
- The indexer lets the object behave like `array[index]`.
- `CheckIndex` protects the invariant that only existing elements are accessed.
- `Array.Resize` creates larger storage when full.
- `Count` increases only after the value is stored.

## 9.4 List trade-offs

| Operation | Typical cost |
|---|---:|
| index access | `O(1)` |
| append | `O(1)` amortized |
| insert at end | `O(1)` amortized |
| insert at beginning | `O(n)` |
| remove by index | `O(n)` if shifting is needed |
| search by value | `O(n)` |

---

# 10. Chapter 9 — Dictionaries and Hash Tables

## 10.1 Key-value lookup

```csharp
Dictionary<int, string> namesById = new();
namesById[101] = "Ari";
namesById[102] = "Bo";

if (namesById.TryGetValue(101, out string? name))
{
    Console.WriteLine(name);
}
```

A dictionary maps each key to a value. Keys must be unique.

## 10.2 Hashing idea

A hash function transforms a key into a number. The dictionary uses that number to choose a storage bucket.

A good hash distribution reduces collisions. A collision occurs when different keys map to the same bucket. The dictionary resolves collisions internally.

## 10.3 Frequency table

```csharp
static Dictionary<string, int> CountWords(IEnumerable<string> words)
{
    Dictionary<string, int> counts = new(StringComparer.OrdinalIgnoreCase);

    foreach (string word in words)
    {
        counts[word] = counts.GetValueOrDefault(word) + 1;
    }

    return counts;
}
```

The comparer makes `C#` and `c#` equal only if the strings are otherwise identical under the chosen comparer.

## 10.4 Custom key equality

For custom keys, implement equality consistently:

```csharp
public sealed record UserKey(int TenantId, int UserId);
```

Records provide value-based equality for their declared data. This makes them useful as dictionary keys when the identity is the combination of those fields.

## 10.5 Dictionary trade-offs

Expected:

- insert: `O(1)`;
- lookup: `O(1)`;
- remove: `O(1)`.

Possible costs:

- extra memory for buckets and entries;
- resizing;
- hash computation;
- unordered iteration unless an ordered structure is selected;
- behavior affected by equality and comparer choices.

---

# 11. Chapter 10 — Sets and Uniqueness

## 11.1 `HashSet<T>`

A set stores unique values:

```csharp
HashSet<string> tags = new(StringComparer.OrdinalIgnoreCase);
tags.Add("data");
tags.Add("Data");
Console.WriteLine(tags.Count); // 1
```

## 11.2 Set operations

```csharp
HashSet<int> left = new() { 1, 2, 3 };
HashSet<int> right = new() { 3, 4, 5 };

HashSet<int> union = left.Union(right).ToHashSet();
HashSet<int> intersection = left.Intersect(right).ToHashSet();
HashSet<int> difference = left.Except(right).ToHashSet();
```

Meaning:

- union: values in either set;
- intersection: values in both sets;
- difference: values in the first set but not the second.

## 11.3 Duplicate detection

```csharp
static bool HasDuplicate<T>(IEnumerable<T> values)
{
    HashSet<T> seen = new();

    foreach (T value in values)
    {
        if (!seen.Add(value))
        {
            return true;
        }
    }

    return false;
}
```

## 11.4 When not to use a set

Do not use a set if:

- duplicates are meaningful;
- insertion order must be preserved and the chosen set does not promise it;
- you need indexed access;
- you need repeated values for counts.

A dictionary of counts may be more appropriate for frequency analysis.

---

# 12. Chapter 11 — Stacks and Queues

## 12.1 Stack: last in, first out

```csharp
Stack<string> undoActions = new();
undoActions.Push("delete row");
undoActions.Push("change title");
string latestAction = undoActions.Pop();
```

The last pushed item is the first popped item.

Use a stack for:

- undo systems;
- call-stack-like processing;
- depth-first traversal;
- expression parsing;
- browser back navigation.

## 12.2 Queue: first in, first out

```csharp
Queue<string> requests = new();
requests.Enqueue("request-1");
requests.Enqueue("request-2");
string next = requests.Dequeue();
```

Use a queue for:

- service requests;
- breadth-first traversal;
- message processing;
- scheduled work.

## 12.3 Implement a queue with a circular array

```csharp
public sealed class CircularQueue<T>
{
    private readonly T[] _items;
    private int _head;
    private int _tail;

    public CircularQueue(int capacity)
    {
        if (capacity <= 0)
        {
            throw new ArgumentOutOfRangeException(nameof(capacity));
        }

        _items = new T[capacity];
    }

    public int Count { get; private set; }

    public void Enqueue(T value)
    {
        if (Count == _items.Length)
        {
            throw new InvalidOperationException("The queue is full.");
        }

        _items[_tail] = value;
        _tail = (_tail + 1) % _items.Length;
        Count++;
    }

    public T Dequeue()
    {
        if (Count == 0)
        {
            throw new InvalidOperationException("The queue is empty.");
        }

        T value = _items[_head];
        _items[_head] = default!;
        _head = (_head + 1) % _items.Length;
        Count--;
        return value;
    }
}
```

The modulo operation wraps an index back to zero when it reaches the array end. This avoids shifting every element after a dequeue.

## 12.4 Complexity

For a well-designed stack or queue:

- push/enqueue: `O(1)`;
- pop/dequeue: `O(1)`;
- peek: `O(1)`.

---

# 13. Chapter 12 — Linked Lists

## 13.1 Node structure

```csharp
public sealed class LinkedNode<T>
{
    public LinkedNode(T value)
    {
        Value = value;
    }

    public T Value { get; }
    public LinkedNode<T>? Next { get; set; }
}
```

A linked list stores nodes connected through references.

## 13.2 Singly linked list

```csharp
public sealed class SimpleLinkedList<T>
{
    private LinkedNode<T>? _head;

    public int Count { get; private set; }

    public void AddFirst(T value)
    {
        LinkedNode<T> node = new(value)
        {
            Next = _head
        };

        _head = node;
        Count++;
    }

    public bool RemoveFirst(out T? value)
    {
        if (_head is null)
        {
            value = default;
            return false;
        }

        value = _head.Value;
        _head = _head.Next;
        Count--;
        return true;
    }
}
```

Adding to the front changes one reference and is `O(1)`. Finding an item by position is `O(n)` because nodes must be followed one by one.

## 13.3 Doubly linked list

A doubly linked node stores both `Next` and `Previous` references. This allows movement in both directions but requires more memory and more pointer updates.

The .NET `LinkedList<T>` provides a doubly linked list. It is useful when you already have a node reference and need efficient insertion or removal around it.

## 13.4 Linked list versus list

| Need | Better starting choice |
|---|---|
| indexed access | `List<T>` |
| compact contiguous storage | `List<T>` |
| append and iteration | `List<T>` often |
| insertion around a known node | linked list |
| frequent random access | `List<T>` |
| learning node-based structures | custom linked list |

A linked list is not automatically faster. Its pointer chasing can be slower in practice even when a particular operation has a favorable asymptotic cost.

---

# 14. Chapter 13 — Priority Queues and Heaps

## 14.1 Priority queue behavior

A normal queue returns the oldest item. A priority queue returns the item with the best priority.

```csharp
PriorityQueue<string, int> work = new();
work.Enqueue("normal task", 10);
work.Enqueue("urgent task", 1);
string next = work.Dequeue();
```

With numeric priorities, confirm whether smaller or larger numbers are considered more urgent. In the .NET default behavior, lower priority values are dequeued first.

## 14.2 Heap idea

A binary heap is a nearly complete tree stored efficiently in an array. For a zero-based array:

- parent of index `i`: `(i - 1) / 2`;
- left child: `2 * i + 1`;
- right child: `2 * i + 2`.

A min-heap keeps the smallest value at the root.

## 14.3 Implement a min-heap

```csharp
public sealed class MinHeap<T> where T : IComparable<T>
{
    private readonly List<T> _items = new();

    public int Count => _items.Count;

    public void Add(T value)
    {
        _items.Add(value);
        BubbleUp(_items.Count - 1);
    }

    public T RemoveMin()
    {
        if (_items.Count == 0)
        {
            throw new InvalidOperationException("The heap is empty.");
        }

        T minimum = _items[0];
        int lastIndex = _items.Count - 1;
        _items[0] = _items[lastIndex];
        _items.RemoveAt(lastIndex);

        if (_items.Count > 0)
        {
            BubbleDown(0);
        }

        return minimum;
    }

    private void BubbleUp(int index)
    {
        while (index > 0)
        {
            int parent = (index - 1) / 2;

            if (_items[parent].CompareTo(_items[index]) <= 0)
            {
                break;
            }

            (_items[parent], _items[index]) =
                (_items[index], _items[parent]);

            index = parent;
        }
    }

    private void BubbleDown(int index)
    {
        while (true)
        {
            int left = index * 2 + 1;
            int right = index * 2 + 2;
            int smallest = index;

            if (left < _items.Count &&
                _items[left].CompareTo(_items[smallest]) < 0)
            {
                smallest = left;
            }

            if (right < _items.Count &&
                _items[right].CompareTo(_items[smallest]) < 0)
            {
                smallest = right;
            }

            if (smallest == index)
            {
                break;
            }

            (_items[index], _items[smallest]) =
                (_items[smallest], _items[index]);

            index = smallest;
        }
    }
}
```

Important invariants:

- every parent is less than or equal to its children;
- the smallest item is at index zero;
- after insertion, bubble up restores the invariant;
- after removal, bubble down restores the invariant.

Complexity:

- add: `O(log n)`;
- remove minimum: `O(log n)`;
- inspect minimum: `O(1)`.

---

# 15. Chapter 14 — Trees and Binary Search Trees

## 15.1 Hierarchical data

Trees represent parent-child relationships:

- file systems;
- organizational charts;
- XML or JSON documents;
- syntax trees;
- product categories;
- decision rules.

## 15.2 Binary tree node

```csharp
public sealed class BinaryTreeNode<T>
{
    public BinaryTreeNode(T value)
    {
        Value = value;
    }

    public T Value { get; }
    public BinaryTreeNode<T>? Left { get; set; }
    public BinaryTreeNode<T>? Right { get; set; }
}
```

Each node has at most two children.

## 15.3 Traversals

In-order traversal:

```csharp
static void InOrder<T>(BinaryTreeNode<T>? node, Action<T> visit)
{
    if (node is null)
    {
        return;
    }

    InOrder(node.Left, visit);
    visit(node.Value);
    InOrder(node.Right, visit);
}
```

Other traversals:

- pre-order: node, left, right;
- in-order: left, node, right;
- post-order: left, right, node;
- level-order: breadth-first by depth.

## 15.4 Binary search tree

A binary search tree maintains an ordering rule. Implementing insertion:

```csharp
public sealed class BinarySearchTree
{
    private BinaryTreeNode<int>? _root;

    public void Insert(int value)
    {
        _root = Insert(_root, value);
    }

    private static BinaryTreeNode<int> Insert(
        BinaryTreeNode<int>? node,
        int value)
    {
        if (node is null)
        {
            return new BinaryTreeNode<int>(value);
        }

        if (value < node.Value)
        {
            node.Left = Insert(node.Left, value);
        }
        else if (value > node.Value)
        {
            node.Right = Insert(node.Right, value);
        }

        return node;
    }
}
```

Duplicate policy matters. This implementation ignores duplicate values. Another design might count duplicates or store them consistently on one side.

## 15.5 Balanced versus unbalanced

A balanced tree keeps height near `log n`. A sequence inserted in sorted order can create a chain with height `n`.

That is why production ordered structures often use self-balancing trees such as red-black trees or B-trees.

---

# 16. Chapter 15 — Balanced Trees and Ordered Data

## 16.1 Ordered dictionaries

.NET provides sorted collections such as:

```csharp
SortedDictionary<string, int> counts = new();
SortedSet<int> sortedValues = new();
```

These maintain sorted order and typically provide `O(log n)` insertion, lookup, and removal.

Use them when you need:

- ordered iteration;
- range queries;
- predecessor or successor operations;
- predictable sorted keys.

## 16.2 Hash table versus balanced tree

| Requirement | Hash structure | Ordered tree |
|---|---|---|
| expected lookup | `O(1)` | `O(log n)` |
| sorted iteration | not primary | yes |
| range query | awkward | natural |
| memory | buckets and entries | nodes or tree entries |
| ordering guarantee | usually no | yes |

## 16.3 B-trees and databases

Databases often use B-tree-like indexes because they reduce disk or page accesses and keep many keys in each node. The same conceptual lesson applies: the best structure depends on the storage medium and access pattern.

## 16.4 Range query thinking

If the question is:

> “Return every timestamp from 10:00 to 11:00.”

A sorted structure can locate the starting position and traverse until the range ends. A hash table can find exact keys but does not naturally support ordered ranges.

---

# 17. Chapter 16 — Graphs

## 17.1 Graph definition

A graph contains vertices and edges. Edges can be:

- directed or undirected;
- weighted or unweighted;
- single or multiple;
- cyclic or acyclic.

## 17.2 Adjacency list

```csharp
Dictionary<string, List<string>> graph = new()
{
    ["A"] = new() { "B", "C" },
    ["B"] = new() { "D" },
    ["C"] = new() { "D" },
    ["D"] = new()
};
```

An adjacency list is space-efficient for sparse graphs.

## 17.3 Adjacency matrix

```csharp
int[,] matrix = new int[4, 4];
matrix[0, 1] = 1;
```

A matrix gives constant-time edge checks but uses `O(V²)` memory. It may be appropriate for dense graphs or very small fixed vertex sets.

## 17.4 Breadth-first graph traversal

```csharp
static List<string> BreadthFirst(
    Dictionary<string, List<string>> graph,
    string start)
{
    List<string> order = new();
    Queue<string> queue = new();
    HashSet<string> visited = new();

    queue.Enqueue(start);
    visited.Add(start);

    while (queue.Count > 0)
    {
        string current = queue.Dequeue();
        order.Add(current);

        foreach (string neighbor in graph[current])
        {
            if (visited.Add(neighbor))
            {
                queue.Enqueue(neighbor);
            }
        }
    }

    return order;
}
```

The queue provides layer-by-layer exploration. The set prevents repeated visits.

## 17.5 Depth-first graph traversal

```csharp
static void DepthFirst(
    Dictionary<string, List<string>> graph,
    string current,
    HashSet<string> visited,
    List<string> order)
{
    if (!visited.Add(current))
    {
        return;
    }

    order.Add(current);

    foreach (string neighbor in graph[current])
    {
        DepthFirst(graph, neighbor, visited, order);
    }
}
```

DFS is useful for connected components, cycle detection, dependency exploration, and backtracking.

## 17.6 Graph structure choice

| Graph characteristic | Good representation |
|---|---|
| sparse graph | adjacency list |
| dense small graph | adjacency matrix |
| weighted edges | neighbor records with weight |
| dynamic node IDs | dictionary keyed by ID |
| repeated shortest-path queries | indexed or preprocessed representation |

---

# 18. Chapter 17 — Immutable and Specialized Structures

## 18.1 Why immutability helps

An immutable collection cannot be changed after creation. Instead of modifying it, an operation returns a new collection.

Benefits:

- fewer hidden side effects;
- easier reasoning;
- safer sharing between components;
- useful for concurrency;
- easier change tracking.

.NET provides types in `System.Collections.Immutable`, such as `ImmutableList<T>` and `ImmutableDictionary<TKey, TValue>`.

## 18.2 Read-only is not always immutable

```csharp
List<int> internalValues = new() { 1, 2, 3 };
IReadOnlyList<int> view = internalValues;
internalValues.Add(4);
```

The read-only view does not expose mutation methods, but the underlying list can still change. True immutability prevents the change itself.

## 18.3 Concurrent collections

For multiple threads, .NET provides:

- `ConcurrentDictionary<TKey, TValue>`;
- `ConcurrentQueue<T>`;
- `ConcurrentStack<T>`;
- `BlockingCollection<T>`.

Thread safety is not just a type choice. You must understand compound operations and whether a sequence of actions is atomic.

## 18.4 Specialized structures

Other useful structures include:

- `BitArray` for compact boolean flags;
- `ArrayPool<T>` for reusing arrays;
- `Memory<T>` for memory-oriented pipelines;
- `Channel<T>` for asynchronous producer-consumer flows;
- `ImmutableArray<T>` for fixed immutable sequences.

Use specialized structures when their guarantees solve a real requirement, not merely because they sound advanced.

---

# 19. Chapter 18 — Data Structures for Data Analysis

This chapter applies data-structure choices to analytical workloads.

## 19.1 Event-log example

Suppose each record contains:

```csharp
public sealed record EventRecord(
    int UserId,
    string EventName,
    DateTime Timestamp,
    double Value);
```

Possible questions:

- how many events occurred?
- how many unique users exist?
- what is the latest event per user?
- which event names are most common?
- what is the average value by event type?
- how many events arrived in each hour?

## 19.2 Structure choices

| Analytical question | Useful structure |
|---|---|
| preserve raw arrival order | `List<EventRecord>` |
| unique users | `HashSet<int>` |
| events by user | `Dictionary<int, List<EventRecord>>` |
| event counts | `Dictionary<string, int>` |
| latest event by user | `Dictionary<int, EventRecord>` |
| process by arrival | `Queue<EventRecord>` |
| top urgent alerts | priority queue |
| ordered time range | sorted dictionary or sorted list |
| relationship network | graph adjacency list |

## 19.3 Grouping by key

```csharp
static Dictionary<string, List<EventRecord>> GroupByEvent(
    IEnumerable<EventRecord> records)
{
    Dictionary<string, List<EventRecord>> groups = new();

    foreach (EventRecord record in records)
    {
        if (!groups.TryGetValue(record.EventName, out List<EventRecord>? list))
        {
            list = new List<EventRecord>();
            groups[record.EventName] = list;
        }

        list.Add(record);
    }

    return groups;
}
```

The dictionary is an index from event name to its records.

## 19.4 Streaming analysis

If the file is too large to load into memory, process one record at a time and maintain only the required state:

- count;
- running sum;
- minimum and maximum;
- frequency dictionary;
- unique-user set.

This changes memory usage from `O(n)` to approximately `O(k)`, where `k` is the number of distinct categories or keys that must be retained.

## 19.5 Data quality and structure design

A missing key, duplicate event, or malformed timestamp must be represented intentionally. Possible policies:

- reject the record;
- store it in an error collection;
- use a special “unknown” key;
- log and continue;
- stop the pipeline.

The data structure should make the chosen policy visible.

---

# 20. Chapter 19 — Build the Data Structure Lab

We now create a complete C# application that demonstrates multiple data structures in one practical workflow.

## 20.1 Create the project

```bash
dotnet new console -n DataStructureLab
cd DataStructureLab
mkdir Models Services
```

Create this structure:

```text
DataStructureLab/
├── Models/
│   └── EventRecord.cs
├── Services/
│   ├── EventAnalyzer.cs
│   └── EventReader.cs
└── Program.cs
```

The application will read CSV rows with this format:

```text
userId,eventName,timestamp,value
101,login,2026-01-01T08:00:00Z,1
102,purchase,2026-01-01T08:03:00Z,49.99
101,logout,2026-01-01T08:10:00Z,1
```

## 20.2 Create the model

Create `Models/EventRecord.cs`:

```csharp
namespace DataStructureLab.Models;

public sealed record EventRecord(
    int UserId,
    string EventName,
    DateTime Timestamp,
    double Value);
```

A record gives value-based equality and concise immutable data. Each event contains four fields.

## 20.3 Create the reader

Create `Services/EventReader.cs`:

```csharp
using System.Globalization;
using DataStructureLab.Models;

namespace DataStructureLab.Services;

public sealed class EventReader
{
    public IReadOnlyList<EventRecord> Read(string path)
    {
        if (!File.Exists(path))
        {
            throw new FileNotFoundException("Event file not found.", path);
        }

        List<EventRecord> events = new();
        string[] lines = File.ReadAllLines(path);

        foreach (string line in lines.Skip(1))
        {
            string[] cells = line.Split(',');

            if (cells.Length != 4)
            {
                continue;
            }

            if (!int.TryParse(cells[0], out int userId))
            {
                continue;
            }

            if (!DateTime.TryParse(
                cells[2],
                CultureInfo.InvariantCulture,
                DateTimeStyles.AssumeUniversal,
                out DateTime timestamp))
            {
                continue;
            }

            if (!double.TryParse(
                cells[3],
                NumberStyles.Float,
                CultureInfo.InvariantCulture,
                out double value))
            {
                continue;
            }

            events.Add(new EventRecord(
                userId,
                cells[1].Trim(),
                timestamp.ToUniversalTime(),
                value));
        }

        return events;
    }
}
```

Line-by-line concepts:

- `File.Exists` validates the external path.
- `List<EventRecord>` preserves file order.
- `Skip(1)` assumes the first row is a header.
- `Split(',')` separates fields in this simple CSV format.
- invalid rows are skipped in this learning version;
- `TryParse` avoids crashing on ordinary bad data;
- `InvariantCulture` gives consistent numeric parsing;
- `ToUniversalTime` normalizes timestamps for comparison;
- the resulting list is exposed as read-only.

A production CSV reader must also handle quoted commas, escaped quotes, line-level diagnostics, and a clear invalid-row policy.

## 20.4 Create the analyzer

Create `Services/EventAnalyzer.cs`:

```csharp
using DataStructureLab.Models;

namespace DataStructureLab.Services;

public sealed class EventAnalyzer
{
    private readonly List<EventRecord> _events;
    private readonly HashSet<int> _uniqueUsers = new();
    private readonly Dictionary<string, int> _eventCounts =
        new(StringComparer.OrdinalIgnoreCase);
    private readonly Dictionary<int, EventRecord> _latestEventByUser = new();
    private readonly Dictionary<int, List<EventRecord>> _eventsByUser = new();

    public EventAnalyzer(IEnumerable<EventRecord> events)
    {
        _events = events.ToList();
        BuildIndexes();
    }

    public int EventCount => _events.Count;

    public int UniqueUserCount => _uniqueUsers.Count;

    public IReadOnlyDictionary<string, int> EventCounts => _eventCounts;

    public IReadOnlyDictionary<int, EventRecord> LatestEventByUser =>
        _latestEventByUser;

    public IReadOnlyList<EventRecord> GetEventsForUser(int userId)
    {
        return _eventsByUser.TryGetValue(userId, out List<EventRecord>? events)
            ? events
            : Array.Empty<EventRecord>();
    }

    private void BuildIndexes()
    {
        foreach (EventRecord record in _events)
        {
            _uniqueUsers.Add(record.UserId);
            _eventCounts[record.EventName] =
                _eventCounts.GetValueOrDefault(record.EventName) + 1;

            if (!_eventsByUser.TryGetValue(
                    record.UserId,
                    out List<EventRecord>? userEvents))
            {
                userEvents = new List<EventRecord>();
                _eventsByUser[record.UserId] = userEvents;
            }

            userEvents.Add(record);

            if (!_latestEventByUser.TryGetValue(
                    record.UserId,
                    out EventRecord? latest) ||
                record.Timestamp > latest.Timestamp)
            {
                _latestEventByUser[record.UserId] = record;
            }
        }
    }
}
```

The analyzer uses several structures because it answers different questions:

- `_events`: ordered raw history;
- `_uniqueUsers`: fast uniqueness and count;
- `_eventCounts`: frequency table;
- `_latestEventByUser`: latest-value index;
- `_eventsByUser`: one-to-many index.

Keeping all indexes correct is the cost of fast queries. If data changes after construction, each index must be updated or rebuilt.

## 20.5 Create the program

Replace `Program.cs` with:

```csharp
using DataStructureLab.Services;

namespace DataStructureLab;

public static class Program
{
    public static void Main(string[] args)
    {
        string path = args.Length > 0 ? args[0] : "events.csv";
        EventReader reader = new();

        try
        {
            EventAnalyzer analyzer = new(reader.Read(path));

            Console.WriteLine("=== Data Structure Lab ===");
            Console.WriteLine($"Events: {analyzer.EventCount}");
            Console.WriteLine($"Unique users: {analyzer.UniqueUserCount}");
            Console.WriteLine();

            Console.WriteLine("Event counts:");
            foreach ((string name, int count) in analyzer.EventCounts
                .OrderByDescending(pair => pair.Value))
            {
                Console.WriteLine($"- {name}: {count}");
            }

            Console.WriteLine();
            Console.Write("Enter a user ID to inspect: ");

            if (int.TryParse(Console.ReadLine(), out int userId))
            {
                Console.WriteLine($"Events for user {userId}:");

                foreach (var record in analyzer.GetEventsForUser(userId))
                {
                    Console.WriteLine(
                        $"- {record.Timestamp:u} " +
                        $"{record.EventName}: {record.Value}");
                }
            }
        }
        catch (FileNotFoundException error)
        {
            Console.WriteLine(error.Message);
        }
    }
}
```

## 20.6 Add sample data

Create `events.csv`:

```text
userId,eventName,timestamp,value
101,login,2026-01-01T08:00:00Z,1
102,purchase,2026-01-01T08:03:00Z,49.99
101,logout,2026-01-01T08:10:00Z,1
103,login,2026-01-01T09:00:00Z,1
101,purchase,2026-01-01T09:15:00Z,19.50
102,logout,2026-01-01T10:00:00Z,1
```

Run:

```bash
dotnet run
```

## 20.7 Analyze the project design

The application pays extra memory to make queries fast:

- raw ordered history costs `O(n)` storage;
- the unique-user set costs `O(u)`;
- event counts cost `O(c)` where `c` is distinct event names;
- user indexes cost `O(n)` references or records.

Construction is approximately `O(n)`. After construction:

- count events: `O(1)`;
- count unique users: `O(1)`;
- event counts: expected `O(1)` lookup per category;
- events for a user: expected `O(1)` index lookup plus `O(k)` output;
- latest event by user: expected `O(1)` lookup.

## 20.8 Improve the project

Implement these improvements one by one:

1. report skipped rows and their line numbers;
2. preserve an invalid-row collection;
3. add a queue for events awaiting processing;
4. add a priority queue for suspicious events;
5. add a sorted dictionary by hour;
6. add a graph of user-to-event relationships;
7. add a streaming reader for large files;
8. add immutable snapshots of reports;
9. add tests for every index;
10. add a database-backed repository.

---

# 21. Chapter 20 — Testing and Benchmarking

## 21.1 Test invariants

For a set:

- adding the same item twice does not increase count;
- removing an absent item does not corrupt the set.

For a queue:

- dequeue order matches enqueue order;
- dequeue from an empty queue is handled clearly.

For a heap:

- each parent has priority no greater than its children;
- repeated removals are sorted by priority.

For an index:

- every raw event is represented in the appropriate index;
- no event is assigned to the wrong key;
- updates affect every relevant index.

## 21.2 Unit-test example

```csharp
[Fact]
public void Analyzer_CountsUniqueUsers()
{
    EventRecord[] events =
    {
        new(1, "login", DateTime.UtcNow, 1),
        new(1, "logout", DateTime.UtcNow, 1),
        new(2, "login", DateTime.UtcNow, 1)
    };

    EventAnalyzer analyzer = new(events);

    Assert.Equal(2, analyzer.UniqueUserCount);
}
```

## 21.3 Property tests

Useful properties include:

- sorting a collection twice produces the same order as sorting once;
- a list's count equals the number of successful additions minus removals;
- a dictionary never returns two values for one key;
- a queue's output order is FIFO;
- a stack's output order is LIFO;
- a tree traversal visits every reachable node exactly once.

## 21.4 Benchmark operations, not unrelated work

If comparing `List<T>` and `LinkedList<T>` insertion, do not include file loading or console printing. Prepare the same input, run only the operation, and measure both time and allocations.

## 21.5 Benchmark realistic workloads

Test:

- small input;
- medium input;
- large input;
- random order;
- sorted order;
- duplicate-heavy data;
- skewed keys;
- repeated queries;
- mixed reads and writes.

An optimization for one workload may be harmful for another.

---

# 22. Chapter 21 — Architecture, Concurrency, and Production

## 22.1 Separate data structures from application rules

Keep collection choices behind a service when possible:

```text
UI → service → repository/indexes → storage
```

This lets you change a list to a dictionary or a JSON file to a database without rewriting the entire user interface.

## 22.2 Multiple indexes and consistency

If one record is stored in three indexes, every mutation must update all three. This creates a consistency risk.

Strategies:

- make records immutable and rebuild indexes;
- centralize mutations in one service;
- use transactions when storage supports them;
- create tests that compare index results with a slow reference scan;
- document which structure is authoritative.

## 22.3 Thread safety

A normal `Dictionary<TKey, TValue>` is not a general-purpose multi-writer concurrent structure. Use locks or concurrent collections when multiple threads access mutable state.

Even with a concurrent dictionary, this may not be atomic as a business operation:

```csharp
if (!dictionary.ContainsKey(key))
{
    dictionary[key] = value;
}
```

Prefer an atomic method such as `GetOrAdd` when that matches the requirement.

## 22.4 Producer-consumer design

A producer creates work and a consumer processes it. A queue or channel connects them.

Requirements to define:

- maximum queue size;
- backpressure behavior;
- shutdown behavior;
- retry policy;
- ordering guarantee;
- duplicate processing policy.

## 22.5 Persistence

In-memory structures disappear when the process ends. For durable data, use:

- files for small tools;
- databases for structured persistent data;
- caches for temporary acceleration;
- object storage for large files.

The in-memory structure may still be used as an index or cache over durable storage.

## 22.6 Security and privacy

Data structures can accidentally retain sensitive data longer than necessary. Consider:

- clearing buffers when appropriate;
- limiting logs;
- applying access control before returning indexed data;
- avoiding exposing internal mutable collections;
- preventing unbounded memory growth from untrusted input.

---

# 23. Chapter 22 — Mastery Roadmap

## Level 1: Fundamental collections

Learn and practice:

- arrays;
- strings;
- `List<T>`;
- `Dictionary<TKey, TValue>`;
- `HashSet<T>`;
- `Stack<T>`;
- `Queue<T>`.

Projects:

1. contact book;
2. inventory list;
3. word-frequency counter;
4. browser-history simulator;
5. customer-service queue.

## Level 2: Custom implementations

Implement:

- dynamic array;
- circular queue;
- linked list;
- stack with an array;
- stack with nodes;
- min-heap;
- binary search tree;
- graph adjacency list.

For each implementation, state invariants and complexity.

## Level 3: Algorithm and structure combinations

Build:

1. autocomplete with a trie;
2. task scheduler with a priority queue;
3. dependency resolver with a graph;
4. cache with a dictionary and linked list;
5. range-query service with an ordered structure;
6. duplicate detector with a hash set;
7. streaming analytics with dictionaries and running totals.

## Level 4: Production design

Learn:

- immutability;
- concurrent collections;
- memory pooling;
- lazy versus eager evaluation;
- database indexes;
- caching;
- serialization;
- performance profiling;
- distributed data structures;
- fault tolerance.

## 23.1 Mastery questions

1. Which operation is most frequent?
2. Is order required?
3. Are duplicates allowed?
4. Is the collection fixed-size?
5. Do I need key lookup or index lookup?
6. Can I afford extra memory for an index?
7. What invariant must always be true?
8. What happens when the collection is empty?
9. What happens when it is full?
10. Is iteration order guaranteed?
11. Is the structure safe across threads?
12. Is the data mutable, immutable, or append-only?
13. Does the workload require exact or approximate results?
14. What is the worst-case complexity?
15. Can a simpler standard .NET type solve the problem?

---

# Appendix A — Complexity Reference

| Structure / operation | Typical time | Notes |
|---|---:|---|
| Array index access | `O(1)` | fixed indexed storage |
| Array search | `O(n)` | unless separately indexed |
| List index access | `O(1)` | backed by array |
| List append | `O(1)` amortized | resize can be `O(n)` |
| List insert/remove middle | `O(n)` | shifts elements |
| Dictionary lookup | `O(1)` expected | depends on hashing and comparer |
| Dictionary insert | `O(1)` expected | resize can be expensive |
| HashSet membership | `O(1)` expected | no duplicates |
| Stack push/pop/peek | `O(1)` | LIFO |
| Queue enqueue/dequeue/peek | `O(1)` | FIFO |
| Linked-list add first | `O(1)` | known endpoint |
| Linked-list search | `O(n)` | sequential traversal |
| Linked-list indexed access | `O(n)` | no random access |
| Heap add/remove | `O(log n)` | root inspection `O(1)` |
| Balanced tree search | `O(log n)` | ordering maintained |
| Unbalanced BST search | `O(n)` worst | can become a chain |
| Graph adjacency-list edge scan | `O(degree)` | proportional to neighbors |
| Graph adjacency-matrix edge check | `O(1)` | memory `O(V²)` |

The word “typical” matters. Analyze the guarantees of the specific implementation and workload.

---

# Appendix B — Vocabulary

| Term | Meaning |
|---|---|
| Adjacency list | A graph representation storing neighbors per vertex |
| Array | Fixed-size indexed sequence |
| Balanced tree | A tree whose height is controlled near logarithmic size |
| Capacity | Allocated storage available before a dynamic structure resizes |
| Collision | Two hash keys mapping to the same bucket |
| Collection | An object that stores multiple values |
| Dequeue | Remove an item from a queue |
| Encapsulation | Keeping data and rules together behind an interface |
| Entry | A key-value record stored in a dictionary-like structure |
| FIFO | First in, first out |
| Graph | Vertices connected by edges |
| Hash function | Function mapping a key to a hash value |
| Heap | Tree-shaped priority structure commonly stored in an array |
| Index | Additional structure that speeds up a query |
| Invariant | A condition that must remain true |
| Iterator | Mechanism for traversing a sequence |
| Key | Identifier used to find a dictionary value |
| LIFO | Last in, first out |
| Linked list | Sequence of nodes connected by references |
| Load factor | Relationship between hash entries and bucket capacity |
| Node | Element containing a value and structural references |
| Queue | FIFO structure |
| Reference | A value that points to an object |
| Set | Collection of unique values |
| Stack | LIFO structure |
| Tree | Hierarchical node structure |
| Vertex | A node in a graph |

---

# Appendix C — Practice Challenges

## Beginner challenges

1. Reverse an array in place.
2. Find the second-largest distinct value.
3. Remove duplicates while preserving order.
4. Count word frequencies.
5. Build a phone book with a dictionary.
6. Simulate browser back and forward actions.
7. Simulate a service queue.
8. Merge two lists.
9. Rotate a list by `k` positions.
10. Validate balanced brackets with a stack.

## Intermediate challenges

1. Implement an LRU cache using a dictionary and linked list.
2. Implement a min-heap.
3. Implement a binary search tree.
4. Find the top `k` frequent values.
5. Group records by multiple keys.
6. Build a graph from an edge file.
7. Find connected components.
8. Detect a cycle.
9. Implement a circular buffer.
10. Build an autocomplete structure.

## Advanced challenges

1. Implement a trie with prefix search.
2. Implement a union-find / disjoint-set structure.
3. Build a concurrent producer-consumer pipeline.
4. Create a time-windowed event index.
5. Design a memory-bounded streaming aggregator.
6. Implement a range-query structure.
7. Compare hash, sorted, and database indexes.
8. Build an append-only event store.
9. Add immutable snapshots to Data Structure Lab.
10. Profile memory allocations and reduce unnecessary copies.

## Final checklist

Before declaring a structure complete:

- [ ] Is its purpose clearly stated?
- [ ] Are its public operations documented?
- [ ] Are its invariants written down?
- [ ] Are empty and full states handled?
- [ ] Are duplicate values handled deliberately?
- [ ] Are invalid indexes rejected?
- [ ] Is mutation controlled?
- [ ] Is the iteration behavior clear?
- [ ] Is equality behavior correct?
- [ ] Is thread safety documented?
- [ ] Are time and memory costs stated?
- [ ] Are tests present for normal and edge cases?
- [ ] Has it been compared with a standard .NET alternative?
- [ ] Was performance measured on a realistic workload?

---

## Final message to the learner

Data structures are not isolated containers to memorize. They are decisions about how information should behave.

> Choose the structure from the operations, protect its invariants, measure its costs, and document its trade-offs.

Start with arrays and lists. Add dictionaries and sets. Learn stacks and queues. Build linked lists, heaps, trees, and graphs yourself. Then use the standard .NET collections in real applications with a clear understanding of what they guarantee.

The path from beginner to mastery is practical:

> Understand the data → identify the operations → choose the representation → implement safely → test invariants → measure performance → improve only when the workload justifies it.
