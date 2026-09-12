# 13 国重计算机程序设计教程

> 适用对象：报考北师大心理学部认知神经科学与学习重点实验室 `081203 计算机应用技术`，已有 Python 基础但需要恢复限时编程能力的考生。

## 1. 考什么，怎样使用本章

[北师大心理学部 2027 年推免综合考核实施细则](https://psych.bnu.edu.cn/xwzx/tzgg/064ffd543231447c86a7ceff7b8797bd.htm)明确：计算机应用技术笔试包含英文文献分析、程序设计和综合素质测评。官网没有公布编程语言、题量和在线评测平台。因此，本章训练可迁移的解题能力，不押某个平台或某套原题。

建议按以下顺序学习：

1. 先掌握第 2 节的六步解题法。
2. 按 T01-T10 顺序手写并运行例题。
3. 关闭教程，完成 [程序设计练习](13_programming_drills.md)。
4. 最后对照 [练习答案](13_programming_answers.md)。

限时笔试中，优先保证正确性。除非题目数据范围要求，不要一开始就追求最复杂的算法。

## 2. 六步解题法

拿到题目后，在草稿纸上固定写六行：

1. **输入输出**：输入是什么，输出是什么？
2. **最小样例**：空输入、单元素、重复元素会怎样？
3. **朴素解法**：最直接的方法是什么，复杂度是多少？
4. **约束判断**：`n` 的范围是否允许朴素解法？
5. **不变量**：循环、窗口、队列或动态规划状态始终保持什么？
6. **验证**：用正常、边界、反例三组数据手推。

常见规模与目标复杂度：

| 输入规模 | 通常可接受的复杂度 |
|---:|---|
| `n <= 20` | `O(2^n)` 或回溯 |
| `n <= 500` | `O(n^2)` |
| `n <= 100000` | `O(n log n)` 或 `O(n)` |
| `n >= 1000000` | 接近 `O(n)` |

## 3. Python 考场骨架

下面的骨架处理空格分隔整数。先读清题目，再决定是否需要它。

```python
def solve(data: str) -> str:
    nums = list(map(int, data.split()))
    return str(sum(nums))


assert solve("1 2 3\n") == "6"
```

高频操作：

| 任务 | Python |
|---|---|
| 排序 | `a.sort()`、`sorted(a)` |
| 计数 | `collections.Counter` |
| 队列 | `collections.deque` |
| 小根堆 | `heapq.heappush/heappop` |
| 无穷大 | `float("inf")` |
| 带下标遍历 | `enumerate(a)` |
| 同时遍历 | `zip(a, b)` |

## 4. T01 哈希：两数之和

### 题目

给定整数数组 `nums` 和目标值 `target`，返回两个不同元素的下标，使它们之和等于目标值。假设恰有一个答案。

### 从朴素到优化

双重循环枚举下标对需要 `O(n^2)`。遍历到 `x` 时，只要知道 `target - x` 是否已经出现，就能立即得到答案。哈希表把查询降为均摊 `O(1)`。

不变量：处理位置 `i` 前，`seen` 保存所有已处理元素到其下标的映射。

```python
def two_sum(nums: list[int], target: int) -> tuple[int, int]:
    seen: dict[int, int] = {}
    for i, x in enumerate(nums):
        need = target - x
        if need in seen:
            return seen[need], i
        seen[x] = i
    raise ValueError("no solution")


assert two_sum([2, 7, 11, 15], 9) == (0, 1)
assert two_sum([3, 3], 6) == (0, 1)
```

手推 `[2, 7, 11, 15]`：读到 `2` 后保存 `{2: 0}`；读到 `7` 时需要 `2`，命中并返回 `(0, 1)`。

- 时间：`O(n)`
- 空间：`O(n)`
- 易错点：先写入再查询会在 `target == 2*x` 时重复使用同一元素。

## 5. T02 排序：合并区间

### 题目

给定若干闭区间，合并所有重叠区间。

### 思路

先按左端点排序。此后，新区间只可能与结果中的最后一个区间重叠。

不变量：`merged` 中的区间有序、互不重叠，并覆盖已经处理的全部区间。

```python
def merge_intervals(intervals: list[list[int]]) -> list[list[int]]:
    if not intervals:
        return []
    intervals = sorted(intervals)
    merged = [intervals[0][:]]
    for left, right in intervals[1:]:
        if left <= merged[-1][1]:
            merged[-1][1] = max(merged[-1][1], right)
        else:
            merged.append([left, right])
    return merged


assert merge_intervals([[1, 3], [2, 6], [8, 10]]) == [[1, 6], [8, 10]]
assert merge_intervals([]) == []
```

- 时间：排序占 `O(n log n)`
- 空间：除输出外取决于排序实现
- 易错点：闭区间用 `left <= last_right`；若题目是开区间，边界规则可能不同。

## 6. T03 二分：第一个不小于目标值的位置

### 题目

在升序数组中，返回第一个大于等于 `target` 的位置；若不存在，返回数组长度。

### 思路

使用左闭右开区间 `[left, right)`。循环始终保证答案位于该区间。

```python
def lower_bound(nums: list[int], target: int) -> int:
    left, right = 0, len(nums)
    while left < right:
        mid = (left + right) // 2
        if nums[mid] < target:
            left = mid + 1
        else:
            right = mid
    return left


assert lower_bound([1, 2, 2, 4], 2) == 1
assert lower_bound([1, 2, 2, 4], 3) == 3
assert lower_bound([1, 2, 2, 4], 5) == 4
```

- 时间：`O(log n)`
- 空间：`O(1)`
- 易错点：不要混用左闭右闭和左闭右开模板。

## 7. T04 栈：括号是否合法

### 题目

字符串只含 `()[]{}`，判断括号是否正确匹配。

### 思路

左括号入栈；右括号必须匹配栈顶。最后栈必须为空。

```python
def valid_parentheses(text: str) -> bool:
    pairs = {")": "(", "]": "[", "}": "{"}
    stack: list[str] = []
    for ch in text:
        if ch in "([{":
            stack.append(ch)
        elif not stack or stack.pop() != pairs[ch]:
            return False
    return not stack


assert valid_parentheses("([]{})")
assert not valid_parentheses("([)]")
assert not valid_parentheses("(")
```

- 时间：`O(n)`
- 空间：最坏 `O(n)`
- 易错点：遇到右括号时先检查空栈，避免 `pop()` 报错。

## 8. T05 滑动窗口：最长无重复子串

### 题目

返回字符串中不含重复字符的最长连续子串长度。

### 思路

`left` 和 `right` 维护当前窗口。若字符上次出现位置仍在窗口内，把左边界跳到其后一位。

```python
def longest_unique_substring(text: str) -> int:
    last: dict[str, int] = {}
    left = 0
    best = 0
    for right, ch in enumerate(text):
        if ch in last and last[ch] >= left:
            left = last[ch] + 1
        last[ch] = right
        best = max(best, right - left + 1)
    return best


assert longest_unique_substring("abcabcbb") == 3
assert longest_unique_substring("abba") == 2
assert longest_unique_substring("") == 0
```

`abba` 是关键反例。读到最后一个 `a` 时，旧 `a` 已经在窗口外，左边界不能后退。

- 时间：`O(n)`
- 空间：`O(k)`，`k` 为字符种类数

## 9. T06 BFS：网格最短路

### 题目

`0` 表示可通行，`1` 表示障碍。每步可上下左右移动，求起点到终点的最少步数；不可达返回 `-1`。

### 思路

无权图的最短路使用广度优先搜索（BFS）。节点第一次入队时就标记访问，防止重复入队。

```python
from collections import deque


def grid_shortest_path(
    grid: list[list[int]], start: tuple[int, int], end: tuple[int, int]
) -> int:
    rows, cols = len(grid), len(grid[0])
    queue = deque([(start[0], start[1], 0)])
    visited = {start}
    while queue:
        row, col, distance = queue.popleft()
        if (row, col) == end:
            return distance
        for dr, dc in ((1, 0), (-1, 0), (0, 1), (0, -1)):
            nr, nc = row + dr, col + dc
            inside = 0 <= nr < rows and 0 <= nc < cols
            if inside and grid[nr][nc] == 0 and (nr, nc) not in visited:
                visited.add((nr, nc))
                queue.append((nr, nc, distance + 1))
    return -1


g = [[0, 0, 1], [1, 0, 0], [0, 0, 0]]
assert grid_shortest_path(g, (0, 0), (2, 2)) == 4
```

- 时间：`O(rows * cols)`
- 空间：`O(rows * cols)`
- 易错点：应在入队时标记访问，而不是出队时。

## 10. T07 DFS：连通分量数量

### 题目

给定无向图节点数 `n` 和边列表，返回连通分量数量。

### 思路

每次从未访问节点开始一次深度优先搜索（DFS），就发现一个新分量。

```python
def count_components(n: int, edges: list[tuple[int, int]]) -> int:
    graph = [[] for _ in range(n)]
    for u, v in edges:
        graph[u].append(v)
        graph[v].append(u)

    visited = [False] * n
    components = 0
    for start in range(n):
        if visited[start]:
            continue
        components += 1
        stack = [start]
        visited[start] = True
        while stack:
            node = stack.pop()
            for nxt in graph[node]:
                if not visited[nxt]:
                    visited[nxt] = True
                    stack.append(nxt)
    return components


assert count_components(5, [(0, 1), (1, 2), (3, 4)]) == 2
assert count_components(3, []) == 3
```

- 时间：`O(V + E)`
- 空间：`O(V + E)`
- 易错点：无向边必须加入两个方向；孤立节点也是一个分量。

## 11. T08 动态规划：不能取相邻元素的最大和

### 题目

给定非负整数数组，选择若干互不相邻元素，使总和最大。

### 状态设计

处理到当前元素时，只需要两个状态：

- `skip`：不取当前元素的最大和。
- `take`：取当前元素的最大和。

转移前必须同时保存旧状态。

```python
def max_non_adjacent_sum(nums: list[int]) -> int:
    skip = 0
    take = 0
    for x in nums:
        new_skip = max(skip, take)
        new_take = skip + x
        skip, take = new_skip, new_take
    return max(skip, take)


assert max_non_adjacent_sum([2, 7, 9, 3, 1]) == 12
assert max_non_adjacent_sum([]) == 0
```

- 时间：`O(n)`
- 空间：`O(1)`
- 易错点：若题目允许负数，要先明确是否可以一个元素也不选。

## 12. T09 堆与最短路：Dijkstra

### 题目

给定非负权有向图，求起点到每个节点的最短距离。

### 思路

小根堆每次取出当前距离最小的节点。若堆中距离不是最新值，跳过该过期条目。

```python
import heapq


def dijkstra(
    n: int, edges: list[tuple[int, int, int]], start: int
) -> list[float]:
    graph = [[] for _ in range(n)]
    for u, v, weight in edges:
        graph[u].append((v, weight))

    distances = [float("inf")] * n
    distances[start] = 0
    heap = [(0, start)]
    while heap:
        distance, node = heapq.heappop(heap)
        if distance != distances[node]:
            continue
        for nxt, weight in graph[node]:
            candidate = distance + weight
            if candidate < distances[nxt]:
                distances[nxt] = candidate
                heapq.heappush(heap, (candidate, nxt))
    return distances


edges = [(0, 1, 4), (0, 2, 1), (2, 1, 2), (1, 3, 1)]
assert dijkstra(4, edges, 0) == [0, 3, 1, 4]
```

- 时间：邻接表加二叉堆为 `O((V + E) log V)`
- 空间：`O(V + E)`
- 易错点：Dijkstra 不能处理负权边。

## 13. T10 科研数据题：状态转移计数

### 题目

给定 HMM 状态序列和状态总数 `k`，计算相邻时刻的转移计数矩阵。矩阵第 `i` 行第 `j` 列表示 `i -> j` 的次数。

### 思路

同时遍历 `states[:-1]` 和 `states[1:]`。长度小于 2 时没有转移。

```python
def transition_counts(states: list[int], k: int) -> list[list[int]]:
    counts = [[0] * k for _ in range(k)]
    for current, nxt in zip(states, states[1:]):
        if not (0 <= current < k and 0 <= nxt < k):
            raise ValueError("state out of range")
        counts[current][nxt] += 1
    return counts


assert transition_counts([0, 1, 1, 2, 0], 3) == [
    [0, 1, 0],
    [0, 1, 1],
    [1, 0, 0],
]
assert transition_counts([0], 2) == [[0, 0], [0, 0]]
```

- 时间：`O(T + k^2)`，初始化矩阵需要 `O(k^2)`
- 空间：`O(k^2)`
- 易错点：转移数是 `T - 1`，不是 `T`；不要把同一状态的连续驻留漏掉。

## 14. 调试清单

提交前逐项检查：

- 空输入和单元素是否有定义？
- 下标是从 `0` 还是从 `1` 开始？
- 是否错误复用同一元素？
- 循环边界是否漏掉最后一个元素？
- BFS 是否在入队时标记访问？
- 图是有向还是无向？权值是否可能为负？
- `float("inf")`、重复值和不可达节点怎样输出？
- 复杂度是否符合数据范围？

## 15. C++17 应试速查

只在考场明确不支持 Python，或你已经熟练掌握 C++ 时切换。

| Python | C++17 |
|---|---|
| `list` | `vector<int>` |
| `dict` | `unordered_map<int, int>` |
| `set` | `unordered_set<int>` |
| `deque` | `queue<int>` / `deque<int>` |
| `heapq` | `priority_queue<T, vector<T>, greater<T>>` |
| `sorted(a)` | `sort(a.begin(), a.end())` |
| `float("inf")` | `numeric_limits<long long>::max()` |

完整输入输出骨架：

```cpp
#include <iostream>
#include <numeric>
#include <vector>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;
    vector<long long> values(n);
    for (long long& value : values) cin >> value;
    cout << accumulate(values.begin(), values.end(), 0LL) << '\n';
    return 0;
}
```

## 16. 七天训练法

| 天数 | 学习 | 闭卷输出 |
|---:|---|---|
| 1 | 哈希、排序、二分 | T01-T03 重写；练习 P01-P04 |
| 2 | 栈、队列、滑动窗口 | T04-T05 重写；练习 P05-P07 |
| 3 | BFS、DFS | T06-T07 重写；练习 P08-P11 |
| 4 | 动态规划 | T08 重写；练习 P12-P14 |
| 5 | 堆、最短路、科研数据 | T09-T10 重写；练习 P15-P16 |
| 6 | 三小时模拟 | 完成 P17，不看答案 |
| 7 | 错题复盘 | 完成 P18；只重做失败题 |

达标标准不是“看懂答案”，而是能在空白编辑器中独立写出、解释复杂度，并用边界样例找到错误。
