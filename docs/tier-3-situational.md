# Tier 3: Situational but High Value C++ Functions & Tools

These functions and data structures are situational, but when needed, they can turn an otherwise complex $O(N^2)$ problem into an elegant $O(N \log N)$ or $O(N)$ solution, or save you from writing hundreds of lines of code.

---

## Table of Contents
41. [`oset` (`find_by_order`, `order_of_key`)](#41-oset-find_by_order-order_of_key)
42. [`__builtin_add_overflow`, `__builtin_mul_overflow`](#42-__builtin_add_overflow-__builtin_mul_overflow)
43. [`partition_point`](#43-partition_point)
44. [`ranges::sort` and C++20 Ranges](#44-rangessort-and-c20-ranges)
45. [`equal_range`](#45-equal_range)
46. [`make_heap`, `push_heap`, `pop_heap`](#46-make_heap-push_heap-pop_heap)
47. [`set_intersection`, `set_union`, `set_difference`](#47-set_intersection-set_union-set_difference)
48. [`transform`, `for_each`](#48-transform-for_each)
49. [`adjacent_difference`](#49-adjacent_difference)
50. [`inner_product`](#50-inner_product)
51. [`clamp`](#51-clamp)
52. [`shuffle`](#52-shuffle)
53. [`partial_sort`](#53-partial_sort)
54. [`lexicographical_compare`](#54-lexicographical_compare)
55. [`bit_width`, `has_single_bit`, `countr_zero`](#55-bit_width-has_single_bit-countr_zero)
56. [`gp_hash_table` (Policy-Based Data Structures)](#56-gp_hash_table-policy-based-data-structures)
57. [`chrono::steady_clock`](#57-chronosteady_clock)
58. [`assert`](#58-assert)

---

### 41. `oset` (`find_by_order`, `order_of_key`)
**What it does:** Policy-based data structure (PB_DS) ordered set that supports finding the $k$-th smallest element (`find_by_order`) and counting elements strictly smaller than $x$ (`order_of_key`) in $O(\log N)$ time.
**Header:** `<ext/pb_ds/assoc_container.hpp>`, `<ext/pb_ds/tree_policy.hpp>`

```cpp
#include <iostream>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>

using namespace __gnu_pbds;
template <typename T>
using ordered_set = tree<T, null_type, std::less<T>, rb_tree_tag, tree_order_statistics_node_update>;

int main() {
    ordered_set<int> s;
    for (int x : {2, 7, 10, 15}) s.insert(x);

    // order_of_key(x): number of elements strictly smaller than x
    std::cout << "Elements < 10: " << s.order_of_key(10) << "\n";

    // find_by_order(k): iterator to k-th element (0-indexed)
    std::cout << "2nd element (0-indexed): " << *s.find_by_order(2) << "\n";
}
```
**Input:** Insert `{2, 7, 10, 15}`
**Output:**
```text
Elements < 10: 2
2nd element (0-indexed): 10
```

---

### 42. `__builtin_add_overflow`, `__builtin_mul_overflow`
**What it does:** Performs arithmetic operations and returns `true` if an overflow occurred, safely writing the wrapped result to an output pointer.
**Header:** Compiler built-in (GCC/Clang)

```cpp
#include <iostream>
#include <climits>

int main() {
    int a = INT_MAX, b = 1, result;
    bool overflow = __builtin_add_overflow(a, b, &result);

    std::cout << "Overflowed? " << std::boolalpha << overflow << "\n";
}
```
**Input:** `a = 2147483647, b = 1`
**Output:** `Overflowed? true`

---

### 43. `partition_point`
**What it does:** Performs binary search on a range partitioned by a predicate to find the first element where the predicate evaluates to `false` in $O(\log N)$ steps.
**Header:** `<algorithm>`

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    // Array partitioned: evens first, then odds
    std::vector<int> nums = {2, 4, 6, 8, 1, 3, 5};
    auto it = std::partition_point(nums.begin(), nums.end(), [](int x) {
        return x % 2 == 0;
    });

    std::cout << "First odd element: " << *it << " at index " << (it - nums.begin()) << "\n";
}
```
**Input:** `nums = [2, 4, 6, 8, 1, 3, 5]`, Predicate: `x % 2 == 0`
**Output:** `First odd element: 1 at index 4`

---

### 44. `ranges::sort` and C++20 Ranges
**What it does:** Modern C++20 range algorithms that eliminate boilerplate `.begin()` and `.end()`, supporting clean projection functions for sorting on struct attributes or pair members.
**Header:** `<algorithm>`, `<vector>`

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

struct Event {
    int time;
    int id;
};

int main() {
    std::vector<Event> events = {{30, 1}, {10, 2}, {20, 3}};
    // Sort entire container by 'time' member directly using projection
    std::ranges::sort(events, {}, &Event::time);

    for (const auto& e : events) {
        std::cout << "{" << e.time << "," << e.id << "} ";
    }
}
```
**Input:** `events = [{30, 1}, {10, 2}, {20, 3}]`
**Output:** `{10,2} {20,3} {30,1} `

---

### 45. `equal_range`
**What it does:** Combines `lower_bound` and `upper_bound` into a single $O(\log N)$ call, returning a pair of iterators `[first, last)` matching a target value in a sorted sequence.
**Header:** `<algorithm>`

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> nums = {1, 2, 4, 4, 4, 5, 9};
    auto [first, last] = std::equal_range(nums.begin(), nums.end(), 4);

    std::cout << "Range of 4 spans indices: [" << (first - nums.begin()) << ", " << (last - nums.begin()) << ")\n";
    std::cout << "Total 4s: " << (last - first) << "\n";
}
```
**Input:** `nums = [1, 2, 4, 4, 4, 5, 9]`, target `4`
**Output:**
```text
Range of 4 spans indices: [2, 5)
Total 4s: 3
```

---

### 46. `make_heap`, `push_heap`, `pop_heap`
**What it does:** Raw binary heap operations directly on contiguous memory (like `std::vector`), avoiding container overhead and enabling fast custom heap manipulations.
**Header:** `<algorithm>`

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> h = {3, 1, 4, 1, 5, 9};
    std::make_heap(h.begin(), h.end()); // Form max-heap: O(N)

    h.push_back(10);
    std::push_heap(h.begin(), h.end()); // Push 10: O(log N)

    std::cout << "Heap top: " << h.front() << "\n";

    std::pop_heap(h.begin(), h.end()); // Moves largest element to back: O(log N)
    h.pop_back();

    std::cout << "New top after pop: " << h.front() << "\n";
}
```
**Input:** Array `[3, 1, 4, 1, 5, 9]`, push `10`, then pop
**Output:**
```text
Heap top: 10
New top after pop: 9
```

---

### 47. `set_intersection`, `set_union`, `set_difference`
**What it does:** Performs classic mathematical set operations on two pre-sorted ranges in linear $O(N + M)$ time.
**Header:** `<algorithm>`

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> a = {1, 2, 3, 5, 7};
    std::vector<int> b = {2, 3, 4, 7, 8};
    std::vector<int> inter;

    std::set_intersection(a.begin(), a.end(), b.begin(), b.end(), std::back_inserter(inter));

    std::cout << "Intersection: ";
    for (int x : inter) std::cout << x << " ";
}
```
**Input:** `a = [1, 2, 3, 5, 7]`, `b = [2, 3, 4, 7, 8]`
**Output:** `Intersection: 2 3 7 `

---

### 48. `transform`, `for_each`
**What it does:** `transform` applies a transformation function across one or two ranges and stores the results; `for_each` executes a side-effecting callable on each element.
**Header:** `<algorithm>`

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> nums = {1, 2, 3, 4};
    std::vector<int> squares(nums.size());

    std::transform(nums.begin(), nums.end(), squares.begin(), [](int x) { return x * x; });

    std::for_each(squares.begin(), squares.end(), [](int x) { std::cout << x << " "; });
}
```
**Input:** `nums = [1, 2, 3, 4]`
**Output:** `1 4 9 16 `

---

### 49. `adjacent_difference`
**What it does:** Computes the difference between each element and its predecessor in $O(N)$ time; effectively computes the difference array (inverse of prefix sum).
**Header:** `<numeric>`

```cpp
#include <iostream>
#include <vector>
#include <numeric>

int main() {
    std::vector<int> pref = {2, 6, 7, 15};
    std::vector<int> diff(pref.size());

    std::adjacent_difference(pref.begin(), pref.end(), diff.begin());

    for (int x : diff) std::cout << x << " ";
}
```
**Input:** `pref = [2, 6, 7, 15]`
**Output:** `2 4 1 8 `

---

### 50. `inner_product`
**What it does:** Computes the sum of products of corresponding elements from two ranges (the dot product) in $O(N)$ time.
**Header:** `<numeric>`

```cpp
#include <iostream>
#include <vector>
#include <numeric>

int main() {
    std::vector<int> a = {1, 3, -5};
    std::vector<int> b = {4, -2, -1};

    int dot_product = std::inner_product(a.begin(), a.end(), b.begin(), 0);
    std::cout << "Dot product: " << dot_product << "\n";
}
```
**Input:** `a = [1, 3, -5]`, `b = [4, -2, -1]`
**Output:** `Dot product: 3` *(1*4 + 3*-2 + -5*-1 = 4 - 6 + 5 = 3)*

---

### 51. `clamp`
**What it does:** Constrains a value within a given lower and upper bound in $O(1)$ time (C++17), equivalent to `max(lo, min(val, hi))`.
**Header:** `<algorithm>`

```cpp
#include <iostream>
#include <algorithm>

int main() {
    std::cout << std::clamp(15, 0, 10) << " ";  // Clamped to upper
    std::cout << std::clamp(-5, 0, 10) << " ";  // Clamped to lower
    std::cout << std::clamp(7, 0, 10) << "\n";  // Within bounds
}
```
**Input:** `(15, 0, 10)`, `(-5, 0, 10)`, `(7, 0, 10)`
**Output:** `10 0 7`

---

### 52. `shuffle`
**What it does:** Randomly reorders elements in a range in $O(N)$ time using a modern random number engine (replaces legacy `std::random_shuffle`).
**Header:** `<algorithm>`, `<random>`

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <random>

int main() {
    std::vector<int> nums = {1, 2, 3, 4, 5};
    std::mt19937 g(42);

    std::shuffle(nums.begin(), nums.end(), g);
    for (int x : nums) std::cout << x << " ";
}
```
**Input:** `nums = [1, 2, 3, 4, 5]`, Seed `42`
**Output:** `2 5 1 3 4 ` *(seeded permutation)*

---

### 53. `partial_sort`
**What it does:** Rearranges elements so that the first $K$ positions hold the smallest $K$ elements in sorted order in $O(N \log K)$ time, faster than full sorting when $K \ll N$.
**Header:** `<algorithm>`

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> nums = {9, 1, 8, 2, 7, 3, 6, 4, 5};
    // Sort only the top 3 smallest elements
    std::partial_sort(nums.begin(), nums.begin() + 3, nums.end());

    std::cout << "Top 3 smallest: ";
    for (int i = 0; i < 3; ++i) std::cout << nums[i] << " ";
}
```
**Input:** `nums = [9, 1, 8, 2, 7, 3, 6, 4, 5]`, $K = 3$
**Output:** `Top 3 smallest: 1 2 3 `

---

### 54. `lexicographical_compare`
**What it does:** Checks if one sequence is lexicographically strictly less than another sequence in $O(\min(N, M))$ time.
**Header:** `<algorithm>`

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> a = {1, 2, 3};
    std::vector<int> b = {1, 2, 4};

    bool is_less = std::lexicographical_compare(a.begin(), a.end(), b.begin(), b.end());
    std::cout << "a < b? " << std::boolalpha << is_less << "\n";
}
```
**Input:** `a = [1, 2, 3]`, `b = [1, 2, 4]`
**Output:** `a < b? true`

---

### 55. `bit_width`, `has_single_bit`, `countr_zero`
**What it does:** Standard C++20 bit-manipulation library (`<bit>`) functions: `bit_width` finds required bits ($\lfloor \log_2(x) \rfloor + 1$), `has_single_bit` checks power of 2, and `countr_zero` counts trailing zeros.
**Header:** `<bit>`

```cpp
#include <iostream>
#include <bit>

int main() {
    unsigned int x = 16;
    std::cout << "has_single_bit(16): " << std::boolalpha << std::has_single_bit(x) << "\n";
    std::cout << "bit_width(16): " << std::bit_width(x) << "\n";
    std::cout << "countr_zero(16): " << std::countr_zero(x) << "\n";
}
```
**Input:** `x = 16`
**Output:**
```text
has_single_bit(16): true
bit_width(16): 5
countr_zero(16): 4
```

---

### 56. `gp_hash_table` (Policy-Based Data Structures)
**What it does:** High-performance hash table from GCC's PB_DS using open-addressing / probing; typically 3x to 6x faster than `std::unordered_map` with lower memory overhead.
**Header:** `<ext/pb_ds/assoc_container.hpp>`

```cpp
#include <iostream>
#include <ext/pb_ds/assoc_container.hpp>

using namespace __gnu_pbds;

int main() {
    gp_hash_table<int, int> fast_map;
    fast_map[42] = 100;
    fast_map[1337] = 200;

    std::cout << "fast_map[42]: " << fast_map[42] << "\n";
}
```
**Input:** Keys `42 -> 100, 1337 -> 200`
**Output:** `fast_map[42]: 100`

---

### 57. `chrono::steady_clock`
**What it does:** Monotonic clock unaffected by system clock adjustments; ideal for benchmarking execution time or enforcing a strict time limit before TLE.
**Header:** `<chrono>`

```cpp
#include <iostream>
#include <chrono>

int main() {
    auto start = std::chrono::steady_clock::now();

    long long sum = 0;
    for (int i = 0; i < 1000000; ++i) sum += i;

    auto end = std::chrono::steady_clock::now();
    std::chrono::duration<double, std::milli> elapsed = end - start;

    std::cout << "Elapsed time: " << (elapsed.count() > 0.0 ? "positive ms" : "0 ms") << "\n";
}
```
**Input:** Loop of $10^6$ operations
**Output:** `Elapsed time: positive ms`

---

### 58. `assert`
**What it does:** Evaluates a boolean expression and immediately aborts program execution with diagnostics if false; invaluable for verifying preconditions, loop invariants, and constraints.
**Header:** `<cassert>`

```cpp
#include <iostream>
#include <cassert>

int divide(int a, int b) {
    assert(b != 0 && "Denominator must be non-zero");
    return a / b;
}

int main() {
    std::cout << "10 / 2 = " << divide(10, 2) << "\n";
}
```
**Input:** `a = 10, b = 2`
**Output:** `10 / 2 = 5`
