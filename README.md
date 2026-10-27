# ⚡ Useful C++ Functions for LeetCode & Competitive Programming

A curated, battle-tested reference guide of built-in C++ functions, STL algorithms, data structures, and language features tailored specifically for **LeetCode** and **competitive programming**.

Stop reinventing standard routines like binary search, heaps, permutations, custom comparators, or bit manipulations during timed contests. Use what the C++ standard library and compiler intrinsics give you for maximum speed and zero boilerplate.

---

## 📚 Tier Overview

Every function includes a **Time & Space Complexity badge in front of the name**, a **1-2 line explanation**, a **self-contained snippet**, and explicit **Input/Output** pairs.

| Tier | Focus | Description | Doc Link |
| :--- | :--- | :--- | :--- |
| **Tier 1** | **Must-Know (Core)** | Functions and data structures you will use in almost every problem. | [**Tier 1 Docs**](docs/tier-1-essentials.md) |
| **Tier 2** | **Very Common** | Fundamental algorithms and utilities for Medium and Hard problems. | [**Tier 2 Docs**](docs/tier-2-common.md) |
| **Tier 3** | **Situational High-Value** | Advanced tools (pb_ds ordered set, ranges, overflow checkers) that trivialize hard problems. | [**Tier 3 Docs**](docs/tier-3-situational.md) |
| **Tier 4** | **Specialized & Rare** | Niche algorithms, bit rotations, zero-allocation views, and geometry math. | [**Tier 4 Docs**](docs/tier-4-specialized.md) |

---

## 🗂️ Quick Index of All 88 Functions (with Time & Space Complexity)

### 🟢 Tier 1: Core Essentials ([Full Guide](docs/tier-1-essentials.md))
1. `[TC: O(N log N) | SC: O(log N)]` [`sort` (with custom comparator / lambda)](docs/tier-1-essentials.md#1-tc-on-log-n--sc-olog-n-sort-with-custom-comparator--lambda) - $O(N \log N)$ sorting with custom lambda conditions.
2. `[TC: O(1) amortized | SC: O(N)]` [`vector`, `pair`, `emplace_back`](docs/tier-1-essentials.md#2-tc-o1-amortized--sc-on-vector-pair-emplace_back) - Dynamic contiguous array and in-place pair construction.
3. `[TC: O(log N) / O(1) | SC: O(N)]` [`map`, `set`, `unordered_map`, `unordered_set`](docs/tier-1-essentials.md#3-tc-olog-n--o1--sc-on-map-set-unordered_map-unordered_set) - Balanced BSTs ($O(\log N)$) vs hash tables ($O(1)$ avg).
4. `[TC: O(log N) | SC: O(N)]` [`priority_queue` (min-heap via `greater<>`)](docs/tier-1-essentials.md#4-tc-olog-n--sc-on-priority_queue-min-heap-via-greater) - Binary heap for top-K and Dijkstra's algorithm.
5. `[TC: O(log N) | SC: O(1)]` [`lower_bound` / `upper_bound`](docs/tier-1-essentials.md#5-tc-olog-n--sc-o1-lower_bound--upper_bound) - $O(\log N)$ binary search for first $\ge x$ and first $> x$.
6. `[TC: O(1) | SC: O(1)]` [`min`, `max`, `swap`](docs/tier-1-essentials.md#6-tc-o1--sc-o1-min-max-swap) - Extremum selection and $O(1)$ variable/container exchange.
7. `[TC: O(N) | SC: O(1)]` [`reverse`](docs/tier-1-essentials.md#7-tc-on--sc-o1-reverse) - In-place sequence reversal.
8. `[TC: O(N) | SC: O(1)]` [`accumulate` (with `0LL`)](docs/tier-1-essentials.md#8-tc-on--sc-o1-accumulate-with-0ll) - Range summation with 64-bit overflow prevention.
9. `[TC: O(1) | SC: O(1)]` [`ios::sync_with_stdio(false); cin.tie(nullptr);`](docs/tier-1-essentials.md#9-tc-o1--sc-o1-iossync_with_stdiofalse-cintienullptr) - Fast I/O to avoid Time Limit Exceeded (TLE).
10. `[TC: O(1) | SC: O(N)]` [`queue`, `stack`, `deque`](docs/tier-1-essentials.md#10-tc-o1--sc-on-queue-stack-deque) - FIFO, LIFO, and double-ended queues for BFS and sliding windows.
11. `[TC: O(1) | SC: O(1)]` [`auto [a, b] = p;` (Structured Bindings)](docs/tier-1-essentials.md#11-tc-o1--sc-o1-auto-a-b--p-structured-bindings) - Clean C++17 unpacking of pairs, tuples, and structs.
12. `[TC: O(1) | SC: O(1)]` [`INT_MAX`, `LLONG_MAX`](docs/tier-1-essentials.md#12-tc-o1--sc-o1-int_max-llong_max) - 32-bit and 64-bit maximum integer sentinel limits.
13. `[TC: O(N) | SC: O(1)]` [`memset`, `fill`](docs/tier-1-essentials.md#13-tc-on--sc-o1-memset-fill) - Fast byte-level block reset vs iterator-based range filling.
14. `[TC: O(len) | SC: O(len)]` [`to_string`, `stoi`, `substr`](docs/tier-1-essentials.md#14-tc-olen--sc-olen-to_string-stoi-substr) - Essential string conversions and slicing.
15. `[TC: O(1) | SC: O(1)]` [`#define all(x)`](docs/tier-1-essentials.md#15-tc-o1--sc-o1-define-allx) - Ubiquitous macro expanding to `(x).begin(), (x).end()`.

---

### 🟡 Tier 2: Very Common ([Full Guide](docs/tier-2-common.md))
16. `[TC: O(N) | SC: O(1)]` [`*min_element`, `*max_element`](docs/tier-2-common.md#16-tc-on--sc-o1-min_element-max_element) - Finds smallest/largest element or its index in a range.
17. `[TC: O(N) | SC: O(1)]` [`unique` + `erase`](docs/tier-2-common.md#17-tc-on--sc-o1-unique--erase) - Removes consecutive duplicates in-place from sorted containers.
18. `[TC: O(N) | SC: O(1)]` [`iota`](docs/tier-2-common.md#18-tc-on--sc-o1-iota) - Populates a sequence with sequentially increasing values (DSU parent array).
19. `[TC: O(log(min(a, b))) | SC: O(1)]` [`gcd`, `lcm`](docs/tier-2-common.md#19-tc-ologmina-b--sc-o1-gcd-lcm) - Greatest common divisor and least common multiple ($O(\log(\min(a, b)))$).
20. `[TC: O(1) | SC: O(1)]` [`__builtin_popcount(ll)`, `__builtin_ctz`, `__builtin_clz`](docs/tier-2-common.md#20-tc-o1--sc-o1-__builtin_popcountll-__builtin_ctz-__builtin_clz) - Hardware-accelerated bit operations (count 1s, trailing zeros, leading zeros).
21. `[TC: O(N) | SC: O(1)]` [`next_permutation`](docs/tier-2-common.md#21-tc-on--sc-o1-next_permutation) - Generates lexicographically next greater sequence in $O(N)$.
22. `[TC: O(N) | SC: O(1)]` [`count`, `count_if`, `find`](docs/tier-2-common.md#22-tc-on--sc-o1-count-count_if-find) - Occurrence counting and element search.
23. `[TC: O(log N) | SC: O(1)]` [`binary_search`](docs/tier-2-common.md#23-tc-olog-n--sc-o1-binary_search) - Returns `true`/`false` for element presence in sorted range in $O(\log N)$.
24. `[TC: O(log N) | SC: O(N)]` [`multiset`](docs/tier-2-common.md#24-tc-olog-n--sc-on-multiset) - Self-balancing BST allowing duplicate keys.
25. `[TC: O(N/64) | SC: O(N/64)]` [`bitset`](docs/tier-2-common.md#25-tc-on64--sc-on64-bitset) - Fixed-size bit array with $64\times$ speedup on bitwise operations (Subset DP).
26. `[TC: O(1) call | SC: O(depth)]` [`function<>` for recursive lambdas`](docs/tier-2-common.md#26-tc-o1-call--sc-odepth-function-for-recursive-lambdas) - Clean in-function recursion for DFS and memoization.
27. `[TC: O(1) | SC: O(1)]` [`tie`, `tuple`](docs/tier-2-common.md#27-tc-o1--sc-o1-tie-tuple) - Heterogeneous tuple storage and simultaneous unpacking.
28. `[TC: O(N) | SC: O(1) aux]` [`partial_sum`](docs/tier-2-common.md#28-tc-on--sc-o1-aux-partial_sum) - Computes prefix sums across a sequence in $O(N)$.
29. `[TC: O(1) | SC: O(1)]` [`sqrt`, `pow`, `abs`, `ceil`, `floor`](docs/tier-2-common.md#29-tc-o1--sc-o1-sqrt-pow-abs-ceil-floor) - Standard mathematical computations.
30. `[TC: O(1) | SC: O(1)]` [`isdigit`, `isalpha`, `tolower`, `toupper`](docs/tier-2-common.md#30-tc-o1--sc-o1-isdigit-isalpha-tolower-toupper) - Character category classification and casing.
31. `[TC: O(L) | SC: O(L)]` [`getline`, `stringstream` / `istringstream`](docs/tier-2-common.md#31-tc-ol--sc-ol-getline-stringstream--istringstream) - Line-based string parsing and whitespace token extraction.
32. `[TC: O(1) | SC: O(1)]` [`mt19937`, `uniform_int_distribution`](docs/tier-2-common.md#32-tc-o1--sc-o1-mt19937-uniform_int_distribution) - Fast pseudo-random number generator to defeat anti-hash tests.
33. `[TC: O(N) | SC: O(1)]` [`rotate`](docs/tier-2-common.md#33-tc-on--sc-o1-rotate) - Left-rotates elements around a pivot in $O(N)$.
34. `[TC: O(N) | SC: O(1)]` [`all_of`, `any_of`, `none_of`](docs/tier-2-common.md#34-tc-on--sc-o1-all_of-any_of-none_of) - Short-circuit predicate testing across ranges.
35. `[TC: O(N) avg | SC: O(log N)]` [`nth_element`](docs/tier-2-common.md#35-tc-on-avg--sc-olog-n-nth_element) - Finds the $k$-th smallest element in $O(N)$ average time.
36. `[TC: O(1) | SC: 16B]` [`__int128`](docs/tier-2-common.md#36-tc-o1--sc-16b-__int128) - 128-bit integer type preventing overflow during intermediate arithmetic.
37. `[TC: O(log N) / O(1) | SC: O(1)]` [`emplace`, `m.contains()`, `try_emplace`](docs/tier-2-common.md#37-tc-olog-n--o1--sc-o1-emplace-mcontains-try_emplace) - Modern associative container insertion and lookup (C++20).
38. `[TC: O(1) | SC: O(1)]` [`rbegin`, `*s.rbegin()`](docs/tier-2-common.md#38-tc-o1--sc-o1-rbegin-srbegin) - Reverse iterator accessing the maximum element of a set/map in $O(1)$.
39. `[TC: O(1) / O(k) | SC: O(1)]` [`next`, `prev`, `distance`](docs/tier-2-common.md#39-tc-o1--ok--sc-o1-next-prev-distance) - Non-modifying iterator offset stepping and distance measurement.
40. `[TC: O(N log N) | SC: O(N)]` [`stable_sort`](docs/tier-2-common.md#40-tc-on-log-n--sc-on-stable_sort) - $O(N \log N)$ sorting preserving relative order of equivalent elements.

---

### 🔵 Tier 3: Situational High-Value ([Full Guide](docs/tier-3-situational.md))
41. `[TC: O(log N) | SC: O(N)]` [`oset` (`find_by_order`, `order_of_key`)](docs/tier-3-situational.md#41-tc-olog-n--sc-on-oset-find_by_order-order_of_key) - Policy-based data structure ordered set with $O(\log N)$ rank lookups.
42. `[TC: O(1) | SC: O(1)]` [`__builtin_add_overflow`, `__builtin_mul_overflow`](docs/tier-3-situational.md#42-tc-o1--sc-o1-__builtin_add_overflow-__builtin_mul_overflow) - Safe arithmetic overflow detection.
43. `[TC: O(log N) | SC: O(1)]` [`partition_point`](docs/tier-3-situational.md#43-tc-olog-n--sc-o1-partition_point) - Binary search on a predicate-partitioned range.
44. `[TC: O(N log N) | SC: O(log N)]` [`ranges::sort` and C++20 Ranges](docs/tier-3-situational.md#44-tc-on-log-n--sc-olog-n-rangessort-and-c20-ranges) - Boilerplate-free sorting with member projections.
45. `[TC: O(log N) | SC: O(1)]` [`equal_range`](docs/tier-3-situational.md#45-tc-olog-n--sc-o1-equal_range) - Single $O(\log N)$ pass returning matching `[lower_bound, upper_bound)` range.
46. `[TC: O(N) / O(log N) | SC: O(1)]` [`make_heap`, `push_heap`, `pop_heap`](docs/tier-3-situational.md#46-tc-on--olog-n--sc-o1-make_heap-push_heap-pop_heap) - Raw in-place heap operations on contiguous vectors.
47. `[TC: O(N + M) | SC: O(1) aux]` [`set_intersection`, `set_union`, `set_difference`](docs/tier-3-situational.md#47-tc-on--m--sc-o1-aux-set_intersection-set_union-set_difference) - Linear $O(N + M)$ mathematical set operations on sorted sequences.
48. `[TC: O(N) | SC: O(1) aux]` [`transform`, `for_each`](docs/tier-3-situational.md#48-tc-on--sc-o1-aux-transform-for_each) - Range transformation and element-wise processing.
49. `[TC: O(N) | SC: O(1) aux]` [`adjacent_difference`](docs/tier-3-situational.md#49-tc-on--sc-o1-aux-adjacent_difference) - Computes difference array (inverse of prefix sum).
50. `[TC: O(N) | SC: O(1)]` [`inner_product`](docs/tier-3-situational.md#50-tc-on--sc-o1-inner_product) - Vector dot product and paired accumulation.
51. `[TC: O(1) | SC: O(1)]` [`clamp`](docs/tier-3-situational.md#51-tc-o1--sc-o1-clamp) - Restricts a value to `[low, high]` in $O(1)$.
52. `[TC: O(N) | SC: O(1)]` [`shuffle`](docs/tier-3-situational.md#52-tc-on--sc-o1-shuffle) - Modern uniform range shuffling via PRNG.
53. `[TC: O(N log K) | SC: O(1)]` [`partial_sort`](docs/tier-3-situational.md#53-tc-on-log-k--sc-o1-partial_sort) - Sorts only the smallest $K$ elements in $O(N \log K)$.
54. `[TC: O(min(N, M)) | SC: O(1)]` [`lexicographical_compare`](docs/tier-3-situational.md#54-tc-ominn-m--sc-o1-lexicographical_compare) - Lexicographical comparison between two sequences.
55. `[TC: O(1) | SC: O(1)]` [`bit_width`, `has_single_bit`, `countr_zero`](docs/tier-3-situational.md#55-tc-o1--sc-o1-bit_width-has_single_bit-countr_zero) - Standard C++20 `<bit>` functions.
56. `[TC: O(1) avg | SC: O(N)]` [`gp_hash_table` (PB_DS)](docs/tier-3-situational.md#56-tc-o1-avg--sc-on-gp_hash_table-pb_ds) - Fast open-addressing hash table (3-5x faster than `std::unordered_map`).
57. `[TC: O(1) | SC: O(1)]` [`chrono::steady_clock`](docs/tier-3-situational.md#57-tc-o1--sc-o1-chronosteady_clock) - Monotonic high-resolution clock to measure runtime and prevent TLE.
58. `[TC: O(1) | SC: O(1)]` [`assert`](docs/tier-3-situational.md#58-tc-o1--sc-o1-assert) - Runtime invariant verification for stress-testing and debugging.

---

### 🟣 Tier 4: Specialized & Rare ([Full Guide](docs/tier-4-specialized.md))
59. `[TC: O(N * M) | SC: O(1)]` [`search`](docs/tier-4-specialized.md#59-tc-on--m--sc-o1-search) - Subsequence pattern matching in sequences.
60. `[TC: O(N) | SC: O(1)]` [`adjacent_find`](docs/tier-4-specialized.md#60-tc-on--sc-o1-adjacent_find) - Finds first pair of consecutive matching elements.
61. `[TC: O(min(N, M)) | SC: O(1)]` [`mismatch`](docs/tier-4-specialized.md#61-tc-ominn-m--sc-o1-mismatch) - Finds the first point of divergence between two ranges.
62. `[TC: O(N^2) / O(N) | SC: O(1)]` [`is_permutation`](docs/tier-4-specialized.md#62-tc-on2--on--sc-o1-is_permutation) - Validates if one range is an arbitrary permutation of another.
63. `[TC: O(N) | SC: O(1)]` [`reduce`](docs/tier-4-specialized.md#63-tc-on--sc-o1-reduce) - Parallel-ready reduction algorithm (C++17).
64. `[TC: O(N) | SC: O(1)]` [`transform_reduce`](docs/tier-4-specialized.md#64-tc-on--sc-o1-transform_reduce) - Fused map-and-reduce single-pass operation (C++17).
65. `[TC: O(N) | SC: O(1) aux]` [`inclusive_scan`](docs/tier-4-specialized.md#65-tc-on--sc-o1-aux-inclusive_scan) - Parallelizable inclusive prefix scan (C++17).
66. `[TC: O(N) | SC: O(1) aux]` [`exclusive_scan`](docs/tier-4-specialized.md#66-tc-on--sc-o1-aux-exclusive_scan) - Parallelizable exclusive prefix scan (C++17).
67. `[TC: O(1) | SC: O(1)]` [`lround`](docs/tier-4-specialized.md#67-tc-o1--sc-o1-lround) - Floating-point rounding to nearest `long int`.
68. `[TC: O(1) | SC: O(1)]` [`atan2`](docs/tier-4-specialized.md#68-tc-o1--sc-o1-atan2) - 4-quadrant arc tangent for 2D geometry and angle sorting.
69. `[TC: O(1) | SC: O(1)]` [`hypot`](docs/tier-4-specialized.md#69-tc-o1--sc-o1-hypot) - Overflow-safe 2D/3D Euclidean distance computation.
70. `[TC: O(1) | SC: O(1)]` [`cbrt`](docs/tier-4-specialized.md#70-tc-o1--sc-o1-cbrt) - Exact cube root supporting negative inputs.
71. `[TC: O(1) | SC: O(1)]` [`fmod`](docs/tier-4-specialized.md#71-tc-o1--sc-o1-fmod) - Floating-point modulo remainder.
72. `[TC: O(N) | SC: O(1) aux]` [`copy_if`](docs/tier-4-specialized.md#72-tc-on--sc-o1-aux-copy_if) - Predicate-filtered range copying.
73. `[TC: O(N) | SC: O(1)]` [`remove_if`](docs/tier-4-specialized.md#73-tc-on--sc-o1-remove_if) - Predicate-filtered in-place element removal.
74. `[TC: O(N) | SC: O(1)]` [`replace`](docs/tier-4-specialized.md#74-tc-on--sc-o1-replace) - Replaces occurrences of an old value with a new value.
75. `[TC: O(N) | SC: O(1)]` [`generate`](docs/tier-4-specialized.md#75-tc-on--sc-o1-generate) - Fills a sequence via repeated invocations of a generator function.
76. `[TC: O(1) | SC: O(1)]` [`exchange`](docs/tier-4-specialized.md#76-tc-o1--sc-o1-exchange) - Replaces variable value and returns previous value.
77. `[TC: O(log N) / O(1) | SC: O(1)]` [`m.extract`](docs/tier-4-specialized.md#77-tc-olog-n--o1--sc-o1-mextract) - Node extraction from map/set to re-key without allocation.
78. `[TC: O(N log(M+N)) | SC: O(1)]` [`m.merge`](docs/tier-4-specialized.md#78-tc-on-logmn--sc-o1-mmerge) - Splices nodes from one container into another in $O(N)$ or $O(N \log M)$.
79. `[TC: O(len) | SC: O(1)]` [`from_chars`](docs/tier-4-specialized.md#79-tc-olen--sc-o1-from_chars) - Ultra-fast, zero-allocation integer and float parsing.
80. `[TC: O(1) | SC: 16B]` [`string_view`](docs/tier-4-specialized.md#80-tc-o1--sc-16b-string_view) - Non-owning string slices with $O(1)$ substring operations.
81. `[TC: O(1) | SC: 16B]` [`span`](docs/tier-4-specialized.md#81-tc-o1--sc-16b-span) - Non-owning bounds-safe contiguous buffer view (C++20).
82. `[TC: O(1) | SC: O(1)]` [`optional`](docs/tier-4-specialized.md#82-tc-o1--sc-o1-optional) - Type-safe optional return value without sentinel hacks.
83. `[TC: O(1) | SC: O(1)]` [`variant`](docs/tier-4-specialized.md#83-tc-o1--sc-o1-variant) - Type-safe tagged union (C++17).
84. `[TC: O(1) lazy | SC: O(1)]` [`views::*`](docs/tier-4-specialized.md#84-tc-o1-lazy--sc-o1-views-c20-ranges) - Composable lazy range adapters (`filter`, `transform`, `take`).
85. `[TC: O(1) | SC: O(1)]` [`rotl`, `rotr`](docs/tier-4-specialized.md#85-tc-o1--sc-o1-rotl-rotr) - CPU bitwise left and right rotations.
86. `[TC: O(1) | SC: O(1)]` [`bit_ceil`](docs/tier-4-specialized.md#86-tc-o1--sc-o1-bit_ceil) - Smallest power of 2 greater than or equal to $x$ (C++20).
87. `[TC: O(N/64) | SC: O(1)]` [`_Find_first`, `_Find_next`](docs/tier-4-specialized.md#87-tc-on64--sc-o1-_find_first-_find_next-stdbitset) - Fast bit iteration on `std::bitset`.
88. `[TC: O(1) | SC: O(N)]` [`list`, `forward_list`](docs/tier-4-specialized.md#88-tc-o1--sc-on-list-forward_list) - Doubly and singly linked lists for $O(1)$ node splicing (LRU cache).

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
