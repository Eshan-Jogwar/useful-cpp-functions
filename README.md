# ⚡ Useful C++ Functions for LeetCode & Competitive Programming

A curated, battle-tested reference guide of built-in C++ functions, STL algorithms, data structures, and language features tailored specifically for **LeetCode** and **competitive programming**.

Stop reinventing standard routines like binary search, heaps, permutations, custom comparators, or bit manipulations during timed contests. Use what the C++ standard library and compiler intrinsics give you for maximum speed and zero boilerplate.

---

## 📚 Tier Overview

Every function includes a **Time & Space Complexity badge `[TC: ... | SC: ...]`**, a **1-2 line explanation**, a **self-contained snippet**, and explicit **Input/Output** pairs.

| Tier | Focus | Description | Doc Link |
| :--- | :--- | :--- | :--- |
| **Tier 1** | **Must-Know (Core)** | Functions and data structures you will use in almost every problem. | [**Tier 1 Docs**](docs/tier-1-essentials.md) |
| **Tier 2** | **Very Common** | Fundamental algorithms and utilities for Medium and Hard problems. | [**Tier 2 Docs**](docs/tier-2-common.md) |
| **Tier 3** | **Situational High-Value** | Advanced tools (pb_ds ordered set, ranges, overflow checkers) that trivialize hard problems. | [**Tier 3 Docs**](docs/tier-3-situational.md) |
| **Tier 4** | **Specialized & Rare** | Niche algorithms, bit rotations, zero-allocation views, and geometry math. | [**Tier 4 Docs**](docs/tier-4-specialized.md) |

---

## 🗂️ Quick Index of All 88 Functions

### 🟢 Tier 1: Core Essentials ([Full Guide](docs/tier-1-essentials.md))
1. [`sort` (with custom comparator / lambda)](docs/tier-1-essentials.md#1-sort-with-custom-comparator--lambda) [TC: O(N log N) | SC: O(log N)] - $O(N \log N)$ sorting with custom lambda conditions.
2. [`vector`, `pair`, `emplace_back`](docs/tier-1-essentials.md#2-vector-pair-emplace_back) [TC: O(1) amortized | SC: O(N)] - Dynamic contiguous array and in-place pair construction.
3. [`map`, `set`, `unordered_map`, `unordered_set`](docs/tier-1-essentials.md#3-map-set-unordered_map-unordered_set) [TC: O(log N) / O(1) | SC: O(N)] - Balanced BSTs ($O(\log N)$) vs hash tables ($O(1)$ avg).
4. [`priority_queue` (min-heap via `greater<>`)](docs/tier-1-essentials.md#4-priority_queue-min-heap-via-greater) [TC: O(log N) | SC: O(N)] - Binary heap for top-K and Dijkstra's algorithm.
5. [`lower_bound` / `upper_bound`](docs/tier-1-essentials.md#5-lower_bound--upper_bound) [TC: O(log N) | SC: O(1)] - $O(\log N)$ binary search for first $\ge x$ and first $> x$.
6. [`min`, `max`, `swap`](docs/tier-1-essentials.md#6-min-max-swap) [TC: O(1) | SC: O(1)] - Extremum selection and $O(1)$ variable/container exchange.
7. [`reverse`](docs/tier-1-essentials.md#7-reverse) [TC: O(N) | SC: O(1)] - In-place sequence reversal.
8. [`accumulate` (with `0LL`)](docs/tier-1-essentials.md#8-accumulate-with-0ll) [TC: O(N) | SC: O(1)] - Range summation with 64-bit overflow prevention.
9. [`ios::sync_with_stdio(false); cin.tie(nullptr);`](docs/tier-1-essentials.md#9-iossync_with_stdiofalse-cintienullptr) [TC: O(1) | SC: O(1)] - Fast I/O to avoid Time Limit Exceeded (TLE).
10. [`queue`, `stack`, `deque`](docs/tier-1-essentials.md#10-queue-stack-deque) [TC: O(1) | SC: O(N)] - FIFO, LIFO, and double-ended queues for BFS and sliding windows.
11. [`auto [a, b] = p;` (Structured Bindings)](docs/tier-1-essentials.md#11-auto-a-b--p-structured-bindings) [TC: O(1) | SC: O(1)] - Clean C++17 unpacking of pairs, tuples, and structs.
12. [`INT_MAX`, `LLONG_MAX`](docs/tier-1-essentials.md#12-int_max-llong_max) [TC: O(1) | SC: O(1)] - 32-bit and 64-bit maximum integer sentinel limits.
13. [`memset`, `fill`](docs/tier-1-essentials.md#13-memset-fill) [TC: O(N) | SC: O(1)] - Fast byte-level block reset vs iterator-based range filling.
14. [`to_string`, `stoi`, `substr`](docs/tier-1-essentials.md#14-to_string-stoi-substr) [TC: O(len) | SC: O(len)] - Essential string conversions and slicing.
15. [`#define all(x)`](docs/tier-1-essentials.md#15-define-allx) [TC: O(1) | SC: O(1)] - Ubiquitous macro expanding to `(x).begin(), (x).end()`.

---

### 🟡 Tier 2: Very Common ([Full Guide](docs/tier-2-common.md))
16. [`*min_element`, `*max_element`](docs/tier-2-common.md#16-min_element-max_element) [TC: O(N) | SC: O(1)] - Finds smallest/largest element or its index in a range.
17. [`unique` + `erase`](docs/tier-2-common.md#17-unique--erase) [TC: O(N) | SC: O(1)] - Removes consecutive duplicates in-place from sorted containers.
18. [`iota`](docs/tier-2-common.md#18-iota) [TC: O(N) | SC: O(1)] - Populates a sequence with sequentially increasing values (DSU parent array).
19. [`gcd`, `lcm`](docs/tier-2-common.md#19-gcd-lcm) [TC: O(log(min(a, b))) | SC: O(1)] - Greatest common divisor and least common multiple ($O(\log(\min(a, b)))$).
20. [`__builtin_popcount(ll)`, `__builtin_ctz`, `__builtin_clz`](docs/tier-2-common.md#20-__builtin_popcountll-__builtin_ctz-__builtin_clz) [TC: O(1) | SC: O(1)] - Hardware-accelerated bit operations (count 1s, trailing zeros, leading zeros).
21. [`next_permutation`](docs/tier-2-common.md#21-next_permutation) [TC: O(N) | SC: O(1)] - Generates lexicographically next greater sequence in $O(N)$.
22. [`count`, `count_if`, `find`](docs/tier-2-common.md#22-count-count_if-find) [TC: O(N) | SC: O(1)] - Occurrence counting and element search.
23. [`binary_search`](docs/tier-2-common.md#23-binary_search) [TC: O(log N) | SC: O(1)] - Returns `true`/`false` for element presence in sorted range in $O(\log N)$.
24. [`multiset`](docs/tier-2-common.md#24-multiset) [TC: O(log N) | SC: O(N)] - Self-balancing BST allowing duplicate keys.
25. [`bitset`](docs/tier-2-common.md#25-bitset) [TC: O(N/64) | SC: O(N/64)] - Fixed-size bit array with $64\times$ speedup on bitwise operations (Subset DP).
26. [`function<>` for recursive lambdas](docs/tier-2-common.md#26-function-for-recursive-lambdas) [TC: O(1) call | SC: O(depth)] - Clean in-function recursion for DFS and memoization.
27. [`tie`, `tuple`](docs/tier-2-common.md#27-tie-tuple) [TC: O(1) | SC: O(1)] - Heterogeneous tuple storage and simultaneous unpacking.
28. [`partial_sum`](docs/tier-2-common.md#28-partial_sum) [TC: O(N) | SC: O(1) aux] - Computes prefix sums across a sequence in $O(N)$.
29. [`sqrt`, `pow`, `abs`, `ceil`, `floor`](docs/tier-2-common.md#29-sqrt-pow-abs-ceil-floor) [TC: O(1) | SC: O(1)] - Standard mathematical computations.
30. [`isdigit`, `isalpha`, `tolower`, `toupper`](docs/tier-2-common.md#30-isdigit-isalpha-tolower-toupper) [TC: O(1) | SC: O(1)] - Character category classification and casing.
31. [`getline`, `stringstream` / `istringstream`](docs/tier-2-common.md#31-getline-stringstream--istringstream) [TC: O(L) | SC: O(L)] - Line-based string parsing and whitespace token extraction.
32. [`mt19937`, `uniform_int_distribution`](docs/tier-2-common.md#32-mt19937-uniform_int_distribution) [TC: O(1) | SC: O(1)] - Fast pseudo-random number generator to defeat anti-hash tests.
33. [`rotate`](docs/tier-2-common.md#33-rotate) [TC: O(N) | SC: O(1)] - Left-rotates elements around a pivot in $O(N)$.
34. [`all_of`, `any_of`, `none_of`](docs/tier-2-common.md#34-all_of-any_of-none_of) [TC: O(N) | SC: O(1)] - Short-circuit predicate testing across ranges.
35. [`nth_element`](docs/tier-2-common.md#35-nth_element) [TC: O(N) avg | SC: O(log N)] - Finds the $k$-th smallest element in $O(N)$ average time.
36. [`__int128`](docs/tier-2-common.md#36-__int128) [TC: O(1) | SC: 16B] - 128-bit integer type preventing overflow during intermediate arithmetic.
37. [`emplace`, `m.contains()`, `try_emplace`](docs/tier-2-common.md#37-emplace-mcontains-try_emplace) [TC: O(log N) / O(1) | SC: O(1)] - Modern associative container insertion and lookup (C++20).
38. [`rbegin`, `*s.rbegin()`](docs/tier-2-common.md#38-rbegin-srbegin) [TC: O(1) | SC: O(1)] - Reverse iterator accessing the maximum element of a set/map in $O(1)$.
39. [`next`, `prev`, `distance`](docs/tier-2-common.md#39-next-prev-distance) [TC: O(1) / O(k) | SC: O(1)] - Non-modifying iterator offset stepping and distance measurement.
40. [`stable_sort`](docs/tier-2-common.md#40-stable_sort) [TC: O(N log N) | SC: O(N)] - $O(N \log N)$ sorting preserving relative order of equivalent elements.

---

### 🔵 Tier 3: Situational High-Value ([Full Guide](docs/tier-3-situational.md))
41. [`oset` (`find_by_order`, `order_of_key`)](docs/tier-3-situational.md#41-oset-find_by_order-order_of_key) [TC: O(log N) | SC: O(N)] - Policy-based data structure ordered set with $O(\log N)$ rank lookups.
42. [`__builtin_add_overflow`, `__builtin_mul_overflow`](docs/tier-3-situational.md#42-__builtin_add_overflow-__builtin_mul_overflow) [TC: O(1) | SC: O(1)] - Safe arithmetic overflow detection.
43. [`partition_point`](docs/tier-3-situational.md#43-partition_point) [TC: O(log N) | SC: O(1)] - Binary search on a predicate-partitioned range.
44. [`ranges::sort` and C++20 Ranges](docs/tier-3-situational.md#44-rangessort-and-c20-ranges) [TC: O(N log N) | SC: O(log N)] - Boilerplate-free sorting with member projections.
45. [`equal_range`](docs/tier-3-situational.md#45-equal_range) [TC: O(log N) | SC: O(1)] - Single $O(\log N)$ pass returning matching `[lower_bound, upper_bound)` range.
46. [`make_heap`, `push_heap`, `pop_heap`](docs/tier-3-situational.md#46-make_heap-push_heap-pop_heap) [TC: O(N) / O(log N) | SC: O(1)] - Raw in-place heap operations on contiguous vectors.
47. [`set_intersection`, `set_union`, `set_difference`](docs/tier-3-situational.md#47-set_intersection-set_union-set_difference) [TC: O(N + M) | SC: O(1) aux] - Linear $O(N + M)$ mathematical set operations on sorted sequences.
48. [`transform`, `for_each`](docs/tier-3-situational.md#48-transform-for_each) [TC: O(N) | SC: O(1) aux] - Range transformation and element-wise processing.
49. [`adjacent_difference`](docs/tier-3-situational.md#49-adjacent_difference) [TC: O(N) | SC: O(1) aux] - Computes difference array (inverse of prefix sum).
50. [`inner_product`](docs/tier-3-situational.md#50-inner_product) [TC: O(N) | SC: O(1)] - Vector dot product and paired accumulation.
51. [`clamp`](docs/tier-3-situational.md#51-clamp) [TC: O(1) | SC: O(1)] - Restricts a value to `[low, high]` in $O(1)$.
52. [`shuffle`](docs/tier-3-situational.md#52-shuffle) [TC: O(N) | SC: O(1)] - Modern uniform range shuffling via PRNG.
53. [`partial_sort`](docs/tier-3-situational.md#53-partial_sort) [TC: O(N log K) | SC: O(1)] - Sorts only the smallest $K$ elements in $O(N \log K)$.
54. [`lexicographical_compare`](docs/tier-3-situational.md#54-lexicographical_compare) [TC: O(min(N, M)) | SC: O(1)] - Lexicographical comparison between two sequences.
55. [`bit_width`, `has_single_bit`, `countr_zero`](docs/tier-3-situational.md#55-bit_width-has_single_bit-countr_zero) [TC: O(1) | SC: O(1)] - Standard C++20 `<bit>` functions.
56. [`gp_hash_table` (PB_DS)](docs/tier-3-situational.md#56-gp_hash_table-policy-based-data-structures) [TC: O(1) avg | SC: O(N)] - Fast open-addressing hash table (3-5x faster than `std::unordered_map`).
57. [`chrono::steady_clock`](docs/tier-3-situational.md#57-chronosteady_clock) [TC: O(1) | SC: O(1)] - Monotonic high-resolution clock to measure runtime and prevent TLE.
58. [`assert`](docs/tier-3-situational.md#58-assert) [TC: O(1) | SC: O(1)] - Runtime invariant verification for stress-testing and debugging.

---

### 🟣 Tier 4: Specialized & Rare ([Full Guide](docs/tier-4-specialized.md))
59. [`search`](docs/tier-4-specialized.md#59-search) [TC: O(N * M) | SC: O(1)] - Subsequence pattern matching in sequences.
60. [`adjacent_find`](docs/tier-4-specialized.md#60-adjacent_find) [TC: O(N) | SC: O(1)] - Finds first pair of consecutive matching elements.
61. [`mismatch`](docs/tier-4-specialized.md#61-mismatch) [TC: O(min(N, M)) | SC: O(1)] - Finds the first point of divergence between two ranges.
62. [`is_permutation`](docs/tier-4-specialized.md#62-is_permutation) [TC: O(N^2) / O(N) | SC: O(1)] - Validates if one range is an arbitrary permutation of another.
63. [`reduce`](docs/tier-4-specialized.md#63-reduce) [TC: O(N) | SC: O(1)] - Parallel-ready reduction algorithm (C++17).
64. [`transform_reduce`](docs/tier-4-specialized.md#64-transform_reduce) [TC: O(N) | SC: O(1)] - Fused map-and-reduce single-pass operation (C++17).
65. [`inclusive_scan`](docs/tier-4-specialized.md#65-inclusive_scan) [TC: O(N) | SC: O(1) aux] - Parallelizable inclusive prefix scan (C++17).
66. [`exclusive_scan`](docs/tier-4-specialized.md#66-exclusive_scan) [TC: O(N) | SC: O(1) aux] - Parallelizable exclusive prefix scan (C++17).
67. [`lround`](docs/tier-4-specialized.md#67-lround) [TC: O(1) | SC: O(1)] - Floating-point rounding to nearest `long int`.
68. [`atan2`](docs/tier-4-specialized.md#68-atan2) [TC: O(1) | SC: O(1)] - 4-quadrant arc tangent for 2D geometry and angle sorting.
69. [`hypot`](docs/tier-4-specialized.md#69-hypot) [TC: O(1) | SC: O(1)] - Overflow-safe 2D/3D Euclidean distance computation.
70. [`cbrt`](docs/tier-4-specialized.md#70-cbrt) [TC: O(1) | SC: O(1)] - Exact cube root supporting negative inputs.
71. [`fmod`](docs/tier-4-specialized.md#71-fmod) [TC: O(1) | SC: O(1)] - Floating-point modulo remainder.
72. [`copy_if`](docs/tier-4-specialized.md#72-copy_if) [TC: O(N) | SC: O(1) aux] - Predicate-filtered range copying.
73. [`remove_if`](docs/tier-4-specialized.md#73-remove_if) [TC: O(N) | SC: O(1)] - Predicate-filtered in-place element removal.
74. [`replace`](docs/tier-4-specialized.md#74-replace) [TC: O(N) | SC: O(1)] - Replaces occurrences of an old value with a new value.
75. [`generate`](docs/tier-4-specialized.md#75-generate) [TC: O(N) | SC: O(1)] - Fills a sequence via repeated invocations of a generator function.
76. [`exchange`](docs/tier-4-specialized.md#76-exchange) [TC: O(1) | SC: O(1)] - Replaces variable value and returns previous value.
77. [`m.extract`](docs/tier-4-specialized.md#77-mextract) [TC: O(log N) / O(1) | SC: O(1)] - Node extraction from map/set to re-key without allocation.
78. [`m.merge`](docs/tier-4-specialized.md#78-mmerge) [TC: O(N log(M+N)) | SC: O(1)] - Splices nodes from one container into another in $O(N)$ or $O(N \log M)$.
79. [`from_chars`](docs/tier-4-specialized.md#79-from_chars) [TC: O(len) | SC: O(1)] - Ultra-fast, zero-allocation integer and float parsing.
80. [`string_view`](docs/tier-4-specialized.md#80-string_view) [TC: O(1) | SC: 16B] - Non-owning string slices with $O(1)$ substring operations.
81. [`span`](docs/tier-4-specialized.md#81-span) [TC: O(1) | SC: 16B] - Non-owning bounds-safe contiguous buffer view (C++20).
82. [`optional`](docs/tier-4-specialized.md#82-optional) [TC: O(1) | SC: O(1)] - Type-safe optional return value without sentinel hacks.
83. [`variant`](docs/tier-4-specialized.md#83-variant) [TC: O(1) | SC: O(1)] - Type-safe tagged union (C++17).
84. [`views::*`](docs/tier-4-specialized.md#84-views-c20-ranges) [TC: O(1) lazy | SC: O(1)] - Composable lazy range adapters (`filter`, `transform`, `take`).
85. [`rotl`, `rotr`](docs/tier-4-specialized.md#85-rotl-rotr) [TC: O(1) | SC: O(1)] - CPU bitwise left and right rotations.
86. [`bit_ceil`](docs/tier-4-specialized.md#86-bit_ceil) [TC: O(1) | SC: O(1)] - Smallest power of 2 greater than or equal to $x$ (C++20).
87. [`_Find_first`, `_Find_next`](docs/tier-4-specialized.md#87-_find_first-_find_next-stdbitset) [TC: O(N/64) | SC: O(1)] - Fast bit iteration on `std::bitset`.
88. [`list`, `forward_list`](docs/tier-4-specialized.md#88-list-forward_list) [TC: O(1) | SC: O(N)] - Doubly and singly linked lists for $O(1)$ node splicing (LRU cache).

---

## 🎯 Categorical Reference Matrix

| Category | Tier 1 | Tier 2 | Tier 3 | Tier 4 |
| :--- | :--- | :--- | :--- | :--- |
| **Containers & DS** | `vector`, `pair`, `map`, `set`, `unordered_map`, `unordered_set`, `priority_queue`, `queue`, `stack`, `deque` | `multiset`, `bitset`, `tuple` | `ordered_set (pb_ds)`, `gp_hash_table (pb_ds)` | `list`, `forward_list`, `span`, `variant`, `optional` |
| **Searching & Sorting** | `sort` (custom lambda), `lower_bound`, `upper_bound` | `binary_search`, `nth_element`, `stable_sort`, `next_permutation` | `partition_point`, `ranges::sort`, `equal_range`, `partial_sort` | `search`, `adjacent_find`, `mismatch`, `is_permutation` |
| **Numeric & Math** | `accumulate (0LL)`, `min`, `max` | `gcd`, `lcm`, `partial_sum`, `sqrt`, `pow`, `abs`, `ceil`, `floor` | `inner_product`, `adjacent_difference`, `clamp` | `reduce`, `transform_reduce`, `inclusive_scan`, `exclusive_scan`, `lround`, `cbrt`, `hypot`, `atan2`, `fmod` |
| **Bit Manipulation** | - | `__builtin_popcount`, `__builtin_ctz`, `__builtin_clz` | `bit_width`, `has_single_bit`, `countr_zero` | `rotl`, `rotr`, `bit_ceil`, `_Find_first`, `_Find_next` |
| **Strings & Parsing** | `to_string`, `stoi`, `substr` | `getline`, `stringstream`, `isdigit`, `isalpha`, `tolower`, `toupper` | - | `from_chars`, `string_view` |
| **Utilities & Tricks** | Fast I/O, Structured Bindings, `INT_MAX`, `memset`/`fill`, `#define all(x)` | `iota`, `unique`+`erase`, `function<>` recursive lambda, `mt19937`, `rotate`, `contains` | `shuffle`, `__builtin_*_overflow`, `make_heap`, `chrono`, `assert` | `generate`, `exchange`, `m.extract`, `m.merge`, `views::*` |

---

## 🚀 LeetCode C++ Boilerplate Template

Paste this at the top of your solution or template for lightning-fast execution and clean syntax:

```cpp
#include <bits/stdc++.h>
using namespace std;

// Speed up standard I/O
static const auto fast_io = []() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    return nullptr;
}();

#define all(x) (x).begin(), (x).end()
#define sz(x) static_cast<int>((x).size())

using ll = long long;
using pii = pair<int, int>;
```

---

## 📄 License
This repository is licensed under the [MIT License](LICENSE).
