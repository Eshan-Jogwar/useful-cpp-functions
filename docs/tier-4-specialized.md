# Tier 4: Specialized & Rare C++ Functions & Features

These functions and language features are rarely required on standard problems, but when an esoteric problem appears (e.g. geometry, bit-level optimizations, non-allocating string parsing, complex ranges), knowing they exist gives you an unfair advantage.

---

## Table of Contents
59. [`search` [TC: O(N * M) | SC: O(1)]](#59-search)
60. [`adjacent_find` [TC: O(N) | SC: O(1)]](#60-adjacent_find)
61. [`mismatch` [TC: O(min(N, M)) | SC: O(1)]](#61-mismatch)
62. [`is_permutation` [TC: O(N^2) / O(N) | SC: O(1)]](#62-is_permutation)
63. [`reduce` [TC: O(N) | SC: O(1)]](#63-reduce)
64. [`transform_reduce` [TC: O(N) | SC: O(1)]](#64-transform_reduce)
65. [`inclusive_scan` [TC: O(N) | SC: O(1) aux]](#65-inclusive_scan)
66. [`exclusive_scan` [TC: O(N) | SC: O(1) aux]](#66-exclusive_scan)
67. [`lround` [TC: O(1) | SC: O(1)]](#67-lround)
68. [`atan2` [TC: O(1) | SC: O(1)]](#68-atan2)
69. [`hypot` [TC: O(1) | SC: O(1)]](#69-hypot)
70. [`cbrt` [TC: O(1) | SC: O(1)]](#70-cbrt)
71. [`fmod` [TC: O(1) | SC: O(1)]](#71-fmod)
72. [`copy_if` [TC: O(N) | SC: O(1) aux]](#72-copy_if)
73. [`remove_if` [TC: O(N) | SC: O(1)]](#73-remove_if)
74. [`replace` [TC: O(N) | SC: O(1)]](#74-replace)
75. [`generate` [TC: O(N) | SC: O(1)]](#75-generate)
76. [`exchange` [TC: O(1) | SC: O(1)]](#76-exchange)
77. [`m.extract` [TC: O(log N) / O(1) | SC: O(1)]](#77-mextract)
78. [`m.merge` [TC: O(N log(M+N)) | SC: O(1)]](#78-mmerge)
79. [`from_chars` [TC: O(len) | SC: O(1)]](#79-from_chars)
80. [`string_view` [TC: O(1) | SC: 16B]](#80-string_view)
81. [`span` [TC: O(1) | SC: 16B]](#81-span)
82. [`optional` [TC: O(1) | SC: O(1)]](#82-optional)
83. [`variant` [TC: O(1) | SC: O(1)]](#83-variant)
84. [`views::*` (C++20 Ranges) [TC: O(1) lazy | SC: O(1)]](#84-views-c20-ranges)
85. [`rotl`, `rotr` [TC: O(1) | SC: O(1)]](#85-rotl-rotr)
86. [`bit_ceil` [TC: O(1) | SC: O(1)]](#86-bit_ceil)
87. [`_Find_first`, `_Find_next` (std::bitset) [TC: O(N/64) | SC: O(1)]](#87-_find_first-_find_next-stdbitset)
88. [`list`, `forward_list` [TC: O(1) | SC: O(N)]](#88-list-forward_list)

---

<a id="59-search"></a>
### 59. `search` [TC: O(N * M) | SC: O(1)]
- **Time Complexity:** $O(N \times M)$ worst-case.
- **Space Complexity:** $O(1)$
- **Header:** `<algorithm>`
- **What it does:** Searches for the first occurrence of a sub-sequence within a sequence in $O(N \times M)$ time.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> text = {1, 2, 3, 4, 5, 6};
    std::vector<int> pattern = {3, 4};

    auto it = std::search(text.begin(), text.end(), pattern.begin(), pattern.end());
    std::cout << "Pattern found at index: " << (it - text.begin()) << "\n";
}
```
**Input:** `text = [1, 2, 3, 4, 5, 6]`, `pattern = [3, 4]`
**Output:** `Pattern found at index: 2`

---

<a id="60-adjacent_find"></a>
### 60. `adjacent_find` [TC: O(N) | SC: O(1)]
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$
- **Header:** `<algorithm>`
- **What it does:** Searches for the first occurrence of two consecutive identical or predicate-satisfying elements in $O(N)$ time.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> nums = {5, 2, 2, 7, 8};
    auto it = std::adjacent_find(nums.begin(), nums.end());

    std::cout << "First duplicate pair starts with: " << *it << " at index " << (it - nums.begin()) << "\n";
}
```
**Input:** `nums = [5, 2, 2, 7, 8]`
**Output:** `First duplicate pair starts with: 2 at index 1`

---

<a id="61-mismatch"></a>
### 61. `mismatch` [TC: O(min(N, M)) | SC: O(1)]
- **Time Complexity:** $O(\min(N, M))$
- **Space Complexity:** $O(1)$
- **Header:** `<algorithm>`
- **What it does:** Compares two ranges simultaneously and returns a pair of iterators pointing to the first differing elements.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> a = {1, 2, 3, 4};
    std::vector<int> b = {1, 2, 9, 4};

    auto [it1, it2] = std::mismatch(a.begin(), a.end(), b.begin());
    std::cout << "Mismatch found: " << *it1 << " vs " << *it2 << "\n";
}
```
**Input:** `a = [1, 2, 3, 4]`, `b = [1, 2, 9, 4]`
**Output:** `Mismatch found: 3 vs 9`

---

<a id="62-is_permutation"></a>
### 62. `is_permutation` [TC: O(N^2) / O(N) | SC: O(1)]
- **Time Complexity:** $O(N^2)$ worst case; $O(N)$ if sequences are already equal.
- **Space Complexity:** $O(1)$
- **Header:** `<algorithm>`
- **What it does:** Checks whether one sequence is a multiset rearrangement (permutation) of another sequence in $O(N^2)$ or $O(N)$ hash time.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> a = {1, 2, 3};
    std::vector<int> b = {3, 1, 2};

    bool match = std::is_permutation(a.begin(), a.end(), b.begin());
    std::cout << "Is permutation? " << std::boolalpha << match << "\n";
}
```
**Input:** `a = [1, 2, 3]`, `b = [3, 1, 2]`
**Output:** `Is permutation? true`

---

<a id="63-reduce"></a>
### 63. `reduce` [TC: O(N) | SC: O(1)]
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$
- **Header:** `<numeric>`
- **What it does:** Out-of-order, parallelizable reduction algorithm (C++17) similar to `accumulate`, but does not require sequential processing.

```cpp
#include <iostream>
#include <vector>
#include <numeric>

int main() {
    std::vector<int> nums = {1, 2, 3, 4, 5};
    int sum = std::reduce(nums.begin(), nums.end(), 0);
    std::cout << "Sum: " << sum << "\n";
}
```
**Input:** `nums = [1, 2, 3, 4, 5]`
**Output:** `Sum: 15`

---

<a id="64-transform_reduce"></a>
### 64. `transform_reduce` [TC: O(N) | SC: O(1)]
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$
- **Header:** `<numeric>`
- **What it does:** Applies a transform operation to range elements and reduces the transformed results in a single fused pass (C++17).

```cpp
#include <iostream>
#include <vector>
#include <numeric>

int main() {
    std::vector<int> nums = {1, 2, 3};
    // Sum of squares: 1^2 + 2^2 + 3^2 = 14
    int sum_sq = std::transform_reduce(nums.begin(), nums.end(), 0, std::plus<>(), [](int x) { return x * x; });
    std::cout << "Sum of squares: " << sum_sq << "\n";
}
```
**Input:** `nums = [1, 2, 3]`
**Output:** `Sum of squares: 14`

---

<a id="65-inclusive_scan"></a>
### 65. `inclusive_scan` [TC: O(N) | SC: O(1) aux]
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$ auxiliary memory.
- **Header:** `<numeric>`
- **What it does:** Computes inclusive prefix sums / prefix operations in $O(N)$ time (the $i$-th output includes element $i$), with parallel support (C++17).

```cpp
#include <iostream>
#include <vector>
#include <numeric>

int main() {
    std::vector<int> nums = {1, 2, 3, 4};
    std::vector<int> out(nums.size());

    std::inclusive_scan(nums.begin(), nums.end(), out.begin());
    for (int x : out) std::cout << x << " ";
}
```
**Input:** `nums = [1, 2, 3, 4]`
**Output:** `1 3 6 10 `

---

<a id="66-exclusive_scan"></a>
### 66. `exclusive_scan` [TC: O(N) | SC: O(1) aux]
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$ auxiliary memory.
- **Header:** `<numeric>`
- **What it does:** Computes exclusive prefix sums in $O(N)$ time where the $i$-th output includes only elements before index $i$ (C++17).

```cpp
#include <iostream>
#include <vector>
#include <numeric>

int main() {
    std::vector<int> nums = {1, 2, 3, 4};
    std::vector<int> out(nums.size());

    std::exclusive_scan(nums.begin(), nums.end(), out.begin(), 0);
    for (int x : out) std::cout << x << " ";
}
```
**Input:** `nums = [1, 2, 3, 4]`, initial value `0`
**Output:** `0 1 3 6 `

---

<a id="67-lround"></a>
### 67. `lround` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(1)$ CPU instruction.
- **Space Complexity:** $O(1)$
- **Header:** `<cmath>`
- **What it does:** Rounds a floating-point number to the nearest integer value of type `long int`, halfway cases rounded away from zero.

```cpp
#include <iostream>
#include <cmath>

int main() {
    std::cout << std::lround(4.4) << " ";
    std::cout << std::lround(4.5) << " ";
    std::cout << std::lround(-2.5) << "\n";
}
```
**Input:** `4.4`, `4.5`, `-2.5`
**Output:** `4 5 -3`

---

<a id="68-atan2"></a>
### 68. `atan2` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(1)$
- **Space Complexity:** $O(1)$
- **Header:** `<cmath>`
- **What it does:** Computes the full 4-quadrant arc tangent $\theta \in (-\pi, \pi]$ of $y/x$, handling division by zero and sign orientation automatically for geometry problems.

```cpp
#include <iostream>
#include <cmath>

int main() {
    double angle = std::atan2(1.0, -1.0); // 135 degrees (3pi/4)
    std::cout << "Angle in radians: " << angle << "\n";
}
```
**Input:** `y = 1.0, x = -1.0`
**Output:** `Angle in radians: 2.35619`

---

<a id="69-hypot"></a>
### 69. `hypot` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(1)$
- **Space Complexity:** $O(1)$
- **Header:** `<cmath>`
- **What it does:** Computes the Euclidean hypotenuse $\sqrt{x^2 + y^2}$ (and 3D $\sqrt{x^2 + y^2 + z^2}$ in C++17) accurately without intermediate underflow or overflow.

```cpp
#include <iostream>
#include <cmath>

int main() {
    double dist2d = std::hypot(3.0, 4.0);
    double dist3d = std::hypot(1.0, 2.0, 2.0); // C++17

    std::cout << "2D: " << dist2d << ", 3D: " << dist3d << "\n";
}
```
**Input:** `(3.0, 4.0)`, `(1.0, 2.0, 2.0)`
**Output:** `2D: 5, 3D: 3`

---

<a id="70-cbrt"></a>
### 70. `cbrt` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(1)$
- **Space Complexity:** $O(1)$
- **Header:** `<cmath>`
- **What it does:** Computes the real cube root $\sqrt[3]{x}$, safely handling negative numbers without returning NaN.

```cpp
#include <iostream>
#include <cmath>

int main() {
    std::cout << "cbrt(27.0): " << std::cbrt(27.0) << "\n";
    std::cout << "cbrt(-8.0): " << std::cbrt(-8.0) << "\n";
}
```
**Input:** `27.0`, `-8.0`
**Output:**
```text
cbrt(27.0): 3
cbrt(-8.0): -2
```

---

<a id="71-fmod"></a>
### 71. `fmod` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(1)$
- **Space Complexity:** $O(1)$
- **Header:** `<cmath>`
- **What it does:** Computes the floating-point remainder of division $x / y$ with the same sign as $x$.

```cpp
#include <iostream>
#include <cmath>

int main() {
    std::cout << "fmod(5.3, 2.0): " << std::fmod(5.3, 2.0) << "\n";
    std::cout << "fmod(-5.3, 2.0): " << std::fmod(-5.3, 2.0) << "\n";
}
```
**Input:** `(5.3, 2.0)`, `(-5.3, 2.0)`
**Output:**
```text
fmod(5.3, 2.0): 1.3
fmod(-5.3, 2.0): -1.3
```

---

<a id="72-copy_if"></a>
### 72. `copy_if` [TC: O(N) | SC: O(1) aux]
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$ auxiliary.
- **Header:** `<algorithm>`
- **What it does:** Copies only the elements from a source range that satisfy a given predicate into a destination container.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> nums = {1, 6, 3, 8, 2, 9};
    std::vector<int> evens;

    std::copy_if(nums.begin(), nums.end(), std::back_inserter(evens), [](int x) {
        return x % 2 == 0;
    });

    for (int x : evens) std::cout << x << " ";
}
```
**Input:** `nums = [1, 6, 3, 8, 2, 9]`
**Output:** `6 8 2 `

---

<a id="73-remove_if"></a>
### 73. `remove_if` [TC: O(N) | SC: O(1)]
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$ in-place shifting.
- **Header:** `<algorithm>`
- **What it does:** Shifts elements that do not satisfy a predicate to the front in $O(N)$ time and returns the past-the-end iterator of remaining elements (use with `.erase()`).

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> nums = {1, 2, 3, 4, 5, 6};
    // Remove all odd numbers
    nums.erase(std::remove_if(nums.begin(), nums.end(), [](int x) { return x % 2 != 0; }), nums.end());

    for (int x : nums) std::cout << x << " ";
}
```
**Input:** `nums = [1, 2, 3, 4, 5, 6]`, remove odd
**Output:** `2 4 6 `

---

<a id="74-replace"></a>
### 74. `replace` [TC: O(N) | SC: O(1)]
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$ in-place.
- **Header:** `<algorithm>`
- **What it does:** Replaces all occurrences of an old value with a new value in a range in $O(N)$ time in-place.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> nums = {1, 2, 0, 4, 0, 5};
    std::replace(nums.begin(), nums.end(), 0, -1);

    for (int x : nums) std::cout << x << " ";
}
```
**Input:** `nums = [1, 2, 0, 4, 0, 5]`, replace `0` with `-1`
**Output:** `1 2 -1 4 -1 5 `

---

<a id="75-generate"></a>
### 75. `generate` [TC: O(N) | SC: O(1)]
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$ auxiliary.
- **Header:** `<algorithm>`
- **What it does:** Populates a range by repeatedly invoking a generator function or stateful lambda.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> powers_of_two(5);
    int current = 1;
    std::generate(powers_of_two.begin(), powers_of_two.end(), [&]() {
        int val = current;
        current *= 2;
        return val;
    });

    for (int x : powers_of_two) std::cout << x << " ";
}
```
**Input:** Vector of size 5
**Output:** `1 2 4 8 16 `

---

<a id="76-exchange"></a>
### 76. `exchange` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(1)$
- **Space Complexity:** $O(1)$
- **Header:** `<utility>`
- **What it does:** Replaces the value of an object with a new value and returns its previous value in $O(1)$ time (C++14).

```cpp
#include <iostream>
#include <utility>

int main() {
    int counter = 10;
    int old_val = std::exchange(counter, 20);

    std::cout << "old: " << old_val << ", new: " << counter << "\n";
}
```
**Input:** `counter = 10`, exchange with `20`
**Output:** `old: 10, new: 20`

---

<a id="77-mextract"></a>
### 77. `m.extract` [TC: O(log N) / O(1) | SC: O(1)]
- **Time Complexity:** `std::map`/`set`: $O(\log N)$; `std::unordered_map`/`set`: $O(1)$ average.
- **Space Complexity:** $O(1)$ (no node allocation/deallocation).
- **Header:** `<map>`, `<set>`
- **What it does:** Unlinks a node from a map or set without allocating/deallocating memory, allowing key alteration without invalidating values (C++17).

```cpp
#include <iostream>
#include <map>
#include <string>

int main() {
    std::map<int, std::string> mp = {{1, "one"}, {2, "two"}};
    auto node = mp.extract(1); // Extract node
    node.key() = 10;           // Change key without reallocation
    mp.insert(std::move(node)); // Reinsert

    for (auto& [k, v] : mp) std::cout << k << ":" << v << " ";
}
```
**Input:** Map `{1: "one", 2: "two"}`, change key `1` to `10`
**Output:** `2:two 10:one `

---

<a id="78-mmerge"></a>
### 78. `m.merge` [TC: O(N log(M+N)) | SC: O(1)]
- **Time Complexity:** Ordered containers: $O(N \log(M + N))$; Unordered containers: $O(N)$ average.
- **Space Complexity:** $O(1)$ auxiliary (node pointer transfers).
- **Header:** `<map>`, `<set>`
- **What it does:** Splices all elements from another container into the current container without copying or allocating new nodes (C++17).

```cpp
#include <iostream>
#include <set>

int main() {
    std::set<int> a = {1, 3, 5};
    std::set<int> b = {2, 4, 6};

    a.merge(b); // b elements transferred into a

    for (int x : a) std::cout << x << " ";
}
```
**Input:** `a = {1, 3, 5}`, `b = {2, 4, 6}`
**Output:** `1 2 3 4 5 6 `

---

<a id="79-from_chars"></a>
### 79. `from_chars` [TC: O(len) | SC: O(1)]
- **Time Complexity:** $O(D)$ where $D$ is the number of processed digit characters.
- **Space Complexity:** $O(1)$ zero memory allocation.
- **Header:** `<charconv>`
- **What it does:** High-performance, zero-allocation, locale-independent string-to-number parser (C++17); up to 10x faster than `stoi`/`sscanf`.

```cpp
#include <iostream>
#include <charconv>
#include <string_view>

int main() {
    std::string_view sv = "987654";
    int val = 0;
    auto [ptr, ec] = std::from_chars(sv.data(), sv.data() + sv.size(), val);

    std::cout << "Parsed value: " << val << "\n";
}
```
**Input:** String view `"987654"`
**Output:** `Parsed value: 987654`

---

<a id="80-string_view"></a>
### 80. `string_view` [TC: O(1) | SC: 16B]
- **Time Complexity:** $O(1)$ construction and substring slicing.
- **Space Complexity:** $O(1)$ (stores only pointer + length, typically 16 bytes).
- **Header:** `<string_view>`
- **What it does:** Non-owning, lightweight view of a character sequence; enables $O(1)$ slicing and sub-string passing without string copying or memory allocation (C++17).

```cpp
#include <iostream>
#include <string_view>

void print_slice(std::string_view sv) {
    std::cout << "Slice: " << sv << " (len: " << sv.size() << ")\n";
}

int main() {
    std::string s = "CompetitiveProgramming";
    print_slice(std::string_view(s).substr(0, 11)); // Zero allocation
}
```
**Input:** String `"CompetitiveProgramming"`, slice `[0, 11)`
**Output:** `Slice: Competitive (len: 11)`

---

<a id="81-span"></a>
### 81. `span` [TC: O(1) | SC: 16B]
- **Time Complexity:** $O(1)$ view creation and subspan indexing.
- **Space Complexity:** $O(1)$ (stores only pointer + size, typically 16 bytes).
- **Header:** `<span>`
- **What it does:** Non-owning view over any contiguous sequence of elements (arrays, vectors) that encapsulates pointer and size safely (C++20).

```cpp
#include <iostream>
#include <span>
#include <vector>

void print_first_two(std::span<const int> s) {
    if (s.size() >= 2) {
        std::cout << s[0] << " " << s[1] << "\n";
    }
}

int main() {
    std::vector<int> v = {10, 20, 30};
    int raw_arr[] = {40, 50, 60};

    print_first_two(v);
    print_first_two(raw_arr);
}
```
**Input:** Vector `{10, 20, 30}`, raw array `{40, 50, 60}`
**Output:**
```text
10 20
40 50
```

---

<a id="82-optional"></a>
### 82. `optional` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(1)$ access, assignment, and boolean checks.
- **Space Complexity:** $O(1)$ (`sizeof(T) + sizeof(bool)`).
- **Header:** `<optional>`
- **What it does:** Manages an optional value that may or may not be present without resorting to sentinel values like `-1` or `nullptr` (C++17).

```cpp
#include <iostream>
#include <optional>
#include <vector>

std::optional<int> find_even(const std::vector<int>& v) {
    for (int x : v) if (x % 2 == 0) return x;
    return std::nullopt;
}

int main() {
    auto res1 = find_even({1, 3, 5});
    auto res2 = find_even({1, 4, 5});

    std::cout << "res1 has value? " << res1.has_value() << "\n";
    std::cout << "res2 value: " << res2.value_or(-1) << "\n";
}
```
**Input:** `{1, 3, 5}` and `{1, 4, 5}`
**Output:**
```text
res1 has value? 0
res2 value: 4
```

---

<a id="83-variant"></a>
### 83. `variant` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(1)$ assignment, visitation, and index retrieval.
- **Space Complexity:** $O(1)$ ($\max(\text{sizeof}(T_i)) + \text{index discriminant}$).
- **Header:** `<variant>`
- **What it does:** Type-safe, union-like container holding a value of one of several specified types with index tracking (C++17).

```cpp
#include <iostream>
#include <variant>
#include <string>

int main() {
    std::variant<int, std::string> v = 42;
    std::cout << "Holds int: " << std::get<int>(v) << "\n";

    v = "hello";
    std::cout << "Holds string: " << std::get<std::string>(v) << "\n";
}
```
**Input:** Assign `42`, then `"hello"`
**Output:**
```text
Holds int: 42
Holds string: hello
```

---

<a id="84-views-c20-ranges"></a>
### 84. `views::*` (C++20 Ranges) [TC: O(1) lazy | SC: O(1)]
- **Time Complexity:** $O(1)$ pipeline creation; $O(1)$ per step on lazy element iteration.
- **Space Complexity:** $O(1)$ zero temporary container allocation.
- **Header:** `<ranges>`
- **What it does:** Lazy, composable range adapters (like `views::iota`, `views::filter`, `views::transform`, `views::take`, `views::reverse`) that process sequences without temporary allocations.

```cpp
#include <iostream>
#include <vector>
#include <ranges>

int main() {
    std::vector<int> nums = {1, 2, 3, 4, 5, 6};

    // Lazily filter evens and square them
    auto pipeline = nums 
        | std::views::filter([](int x) { return x % 2 == 0; })
        | std::views::transform([](int x) { return x * x; });

    for (int x : pipeline) std::cout << x << " ";
}
```
**Input:** `nums = [1, 2, 3, 4, 5, 6]`
**Output:** `4 16 36 `

---

<a id="85-rotl-rotr"></a>
### 85. `rotl`, `rotr` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(1)$ single CPU bit-rotation instruction.
- **Space Complexity:** $O(1)$
- **Header:** `<bit>`
- **What it does:** Bitwise rotates an unsigned integer left (`rotl`) or right (`rotr`) by $s$ bits in $O(1)$ hardware instructions (C++20).

```cpp
#include <iostream>
#include <bit>
#include <cstdint>

int main() {
    uint8_t x = 0b00000001;
    uint8_t rotated = std::rotl(x, 2); // Rotates left by 2 bits

    std::cout << "rotl(1, 2) = " << (int)rotated << "\n";
}
```
**Input:** `x = 1 (0b00000001)`, shift `2`
**Output:** `rotl(1, 2) = 4`

---

<a id="86-bit_ceil"></a>
### 86. `bit_ceil` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(1)$ single CPU instruction.
- **Space Complexity:** $O(1)$
- **Header:** `<bit>`
- **What it does:** Finds the smallest power of 2 greater than or equal to a given unsigned integer $x$ in $O(1)$ (C++20).

```cpp
#include <iostream>
#include <bit>

int main() {
    std::cout << "bit_ceil(5): " << std::bit_ceil(5u) << "\n";
    std::cout << "bit_ceil(16): " << std::bit_ceil(16u) << "\n";
    std::cout << "bit_ceil(17): " << std::bit_ceil(17u) << "\n";
}
```
**Input:** `5, 16, 17`
**Output:**
```text
bit_ceil(5): 8
bit_ceil(16): 16
bit_ceil(17): 32
```

---

<a id="87-_find_first-_find_next-stdbitset"></a>
### 87. `_Find_first`, `_Find_next` (`std::bitset`) [TC: O(N/64) | SC: O(1)]
- **Time Complexity:** $O(N/64)$ word-level checks; jumps directly to next set bit.
- **Space Complexity:** $O(1)$
- **Header:** `<bitset>`
- **What it does:** Internal GCC extension methods on `std::bitset` that find the first set bit and next set bit efficiently, skipping blocks of 64 zeros.

```cpp
#include <iostream>
#include <bitset>

int main() {
    std::bitset<64> b;
    b.set(4);
    b.set(19);

    size_t first = b._Find_first();
    size_t next = b._Find_next(first);

    std::cout << "Set bit indices: " << first << " and " << next << "\n";
}
```
**Input:** `bitset` with bits 4 and 19 set
**Output:** `Set bit indices: 4 and 19`

---

<a id="88-list-forward_list"></a>
### 88. `list`, `forward_list` [TC: O(1) | SC: O(N)]
- **Time Complexity:** $O(1)$ for insertion, deletion, and splicing with given iterator.
- **Space Complexity:** $O(N)$ with per-node pointer overhead (2 pointers for `list`, 1 pointer for `forward_list`).
- **Header:** `<list>`, `<forward_list>`
- **What it does:** Node-based linked lists (`list` is doubly-linked, `forward_list` is singly-linked); supports $O(1)$ splicing and node insertion/removal without iterator invalidation (essential for LRU cache).

```cpp
#include <iostream>
#include <list>

int main() {
    std::list<int> l = {1, 2, 4};
    auto it = l.begin();
    std::advance(it, 2); // points to 4
    l.insert(it, 3);     // Insert 3 before 4 in O(1)

    for (int x : l) std::cout << x << " ";
}
```
**Input:** `l = [1, 2, 4]`, insert `3` before `4`
**Output:** `1 2 3 4 `
