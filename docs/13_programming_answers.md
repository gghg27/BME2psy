# 13 程序设计专项练习参考答案

> 先完成 [题目](13_programming_drills.md)。答案给出一种可靠实现，不代表唯一写法。

## P01 词频最高的编号

模式是哈希计数。`min` 的排序键先比较负频数，再比较数值。

```python
from collections import Counter


def most_frequent(nums: list[int]) -> int | None:
    if not nums:
        return None
    counts = Counter(nums)
    return min(counts, key=lambda x: (-counts[x], x))


assert most_frequent([4, 2, 4, 2, 2]) == 2
assert most_frequent([3, 1, 3, 1]) == 1
assert most_frequent([]) is None
```

时间 `O(n)`，空间 `O(k)`。不要依赖字典插入顺序处理并列规则。

## P02 去重并保持顺序

集合负责判重，结果列表负责保存顺序。

```python
def unique_in_order(nums: list[int]) -> list[int]:
    seen: set[int] = set()
    result = []
    for x in nums:
        if x not in seen:
            seen.add(x)
            result.append(x)
    return result


assert unique_in_order([3, 1, 3, 2, 1]) == [3, 1, 2]
assert unique_in_order([]) == []
```

时间 `O(n)`，空间 `O(k)`。

## P03 三数之和

排序后固定第一个数，对剩余部分使用双指针。排序让去重和指针移动都有明确方向。

```python
def three_sum(nums: list[int]) -> list[list[int]]:
    nums = sorted(nums)
    result: list[list[int]] = []
    for i in range(len(nums) - 2):
        if i > 0 and nums[i] == nums[i - 1]:
            continue
        if nums[i] > 0:
            break
        left, right = i + 1, len(nums) - 1
        while left < right:
            total = nums[i] + nums[left] + nums[right]
            if total < 0:
                left += 1
            elif total > 0:
                right -= 1
            else:
                result.append([nums[i], nums[left], nums[right]])
                left += 1
                right -= 1
                while left < right and nums[left] == nums[left - 1]:
                    left += 1
                while left < right and nums[right] == nums[right + 1]:
                    right -= 1
    return result


assert three_sum([-1, 0, 1, 2, -1, -4]) == [[-1, -1, 2], [-1, 0, 1]]
assert three_sum([0, 0, 0, 0]) == [[0, 0, 0]]
```

时间 `O(n^2)`，空间不计输出通常为排序所需空间。外层和内层都要去重。

## P04 旋转数组中的最小值

若中点大于最右元素，最小值在右半部分；否则中点可能就是答案。

```python
def rotated_min(nums: list[int]) -> int:
    left, right = 0, len(nums) - 1
    while left < right:
        mid = (left + right) // 2
        if nums[mid] > nums[right]:
            left = mid + 1
        else:
            right = mid
    return nums[left]


assert rotated_min([4, 5, 1, 2, 3]) == 1
assert rotated_min([1, 2, 3]) == 1
assert rotated_min([2]) == 2
```

时间 `O(log n)`，空间 `O(1)`。本解法依赖“无重复元素”。

## P05 每日温度

单调栈保存尚未找到更高温度的下标，栈内对应温度单调不增。

```python
def daily_temperatures(values: list[int]) -> list[int]:
    result = [0] * len(values)
    stack: list[int] = []
    for i, value in enumerate(values):
        while stack and values[stack[-1]] < value:
            previous = stack.pop()
            result[previous] = i - previous
        stack.append(i)
    return result


assert daily_temperatures([73, 74, 75, 71, 69, 72, 76, 73]) == [1, 1, 4, 2, 1, 1, 0, 0]
assert daily_temperatures([3, 2, 1]) == [0, 0, 0]
```

每个下标最多入栈、出栈一次，时间 `O(n)`，空间 `O(n)`。

## P06 长度最小的连续子数组

正整数保证右端扩张时总和不减，左端收缩时总和不增，因此滑动窗口成立。

```python
def min_subarray_len(target: int, nums: list[int]) -> int:
    left = 0
    total = 0
    best = len(nums) + 1
    for right, x in enumerate(nums):
        total += x
        while total >= target:
            best = min(best, right - left + 1)
            total -= nums[left]
            left += 1
    return 0 if best == len(nums) + 1 else best


assert min_subarray_len(7, [2, 3, 1, 2, 4, 3]) == 2
assert min_subarray_len(8, [1, 1, 1]) == 0
```

时间 `O(n)`，空间 `O(1)`。数组含负数时不能使用该单调窗口逻辑。

## P07 移动平均

维护窗口和，每次加入新值并移除离开窗口的值。

```python
def moving_average(values: list[float], k: int) -> list[float]:
    if k <= 0 or k > len(values):
        return []
    window_sum = sum(values[:k])
    result = [window_sum / k]
    for right in range(k, len(values)):
        window_sum += values[right] - values[right - k]
        result.append(window_sum / k)
    return result


assert moving_average([1, 2, 3, 6], 3) == [2.0, 11 / 3]
assert moving_average([1, 2], 3) == []
```

时间 `O(n)`，输出外空间 `O(1)`。

## P08 岛屿数量

每遇到未访问陆地就发现一个新岛，并用栈标记整座岛。

```python
def count_islands(grid: list[list[str]]) -> int:
    if not grid:
        return 0
    rows, cols = len(grid), len(grid[0])
    visited: set[tuple[int, int]] = set()
    islands = 0
    for row in range(rows):
        for col in range(cols):
            if grid[row][col] != "1" or (row, col) in visited:
                continue
            islands += 1
            stack = [(row, col)]
            visited.add((row, col))
            while stack:
                r, c = stack.pop()
                for dr, dc in ((1, 0), (-1, 0), (0, 1), (0, -1)):
                    nr, nc = r + dr, c + dc
                    if 0 <= nr < rows and 0 <= nc < cols:
                        if grid[nr][nc] == "1" and (nr, nc) not in visited:
                            visited.add((nr, nc))
                            stack.append((nr, nc))
    return islands


g = [["1", "1", "0"], ["0", "1", "0"], ["1", "0", "1"]]
assert count_islands(g) == 3
assert count_islands([]) == 0
```

时间和空间均为 `O(rows * cols)`。迭代版不会触发 Python 递归深度限制。

## P09 二分图判断

用 `1/-1` 染色。图不连通，所以每个未染色节点都要启动一次 BFS。

```python
from collections import deque


def is_bipartite(graph: list[list[int]]) -> bool:
    color = [0] * len(graph)
    for start in range(len(graph)):
        if color[start] != 0:
            continue
        color[start] = 1
        queue = deque([start])
        while queue:
            node = queue.popleft()
            for nxt in graph[node]:
                if color[nxt] == 0:
                    color[nxt] = -color[node]
                    queue.append(nxt)
                elif color[nxt] == color[node]:
                    return False
    return True


assert is_bipartite([[1, 3], [0, 2], [1, 3], [0, 2]])
assert not is_bipartite([[1, 2], [0, 2], [0, 1]])
```

时间 `O(V + E)`，空间 `O(V)`。

## P10 课程安排

拓扑排序每次取入度为零的课程。若最终处理数小于 `n`，图中存在环。

```python
from collections import deque


def course_order(n: int, prerequisites: list[tuple[int, int]]) -> list[int]:
    graph = [[] for _ in range(n)]
    indegree = [0] * n
    for course, prerequisite in prerequisites:
        graph[prerequisite].append(course)
        indegree[course] += 1
    queue = deque(i for i, degree in enumerate(indegree) if degree == 0)
    order = []
    while queue:
        node = queue.popleft()
        order.append(node)
        for nxt in graph[node]:
            indegree[nxt] -= 1
            if indegree[nxt] == 0:
                queue.append(nxt)
    return order if len(order) == n else []


assert course_order(2, [(1, 0)]) == [0, 1]
assert course_order(2, [(1, 0), (0, 1)]) == []
```

时间 `O(V + E)`，空间 `O(V + E)`。边方向应为“先修课指向后续课程”。

## P11 带权网格最小代价

把网格视为非负权图，使用 Dijkstra。进入邻格时增加邻格代价。

```python
import heapq


def min_grid_cost(grid: list[list[int]]) -> int:
    rows, cols = len(grid), len(grid[0])
    dist = [[float("inf")] * cols for _ in range(rows)]
    dist[0][0] = grid[0][0]
    heap = [(grid[0][0], 0, 0)]
    while heap:
        cost, row, col = heapq.heappop(heap)
        if cost != dist[row][col]:
            continue
        if (row, col) == (rows - 1, cols - 1):
            return cost
        for dr, dc in ((1, 0), (-1, 0), (0, 1), (0, -1)):
            nr, nc = row + dr, col + dc
            if 0 <= nr < rows and 0 <= nc < cols:
                candidate = cost + grid[nr][nc]
                if candidate < dist[nr][nc]:
                    dist[nr][nc] = candidate
                    heapq.heappush(heap, (candidate, nr, nc))
    raise RuntimeError("unreachable")


assert min_grid_cost([[1, 3, 1], [1, 5, 1], [4, 2, 1]]) == 7
```

时间 `O(RC log(RC))`，空间 `O(RC)`。

## P12 爬楼梯

到达当前台阶的方法数等于前两级之和。

```python
def climb_stairs(n: int) -> int:
    previous, current = 1, 1
    for _ in range(n):
        previous, current = current, previous + current
    return previous


assert climb_stairs(0) == 1
assert climb_stairs(2) == 2
assert climb_stairs(5) == 8
```

时间 `O(n)`，空间 `O(1)`。

## P13 最少硬币数

`dp[value]` 表示凑出 `value` 的最少硬币数。最后一步选硬币 `coin`，前一状态是 `value - coin`。

```python
def min_coins(coins: list[int], amount: int) -> int:
    dp = [amount + 1] * (amount + 1)
    dp[0] = 0
    for value in range(1, amount + 1):
        for coin in coins:
            if coin <= value:
                dp[value] = min(dp[value], dp[value - coin] + 1)
    return -1 if dp[amount] == amount + 1 else dp[amount]


assert min_coins([1, 2, 5], 11) == 3
assert min_coins([2], 3) == -1
assert min_coins([2], 0) == 0
```

时间 `O(amount * len(coins))`，空间 `O(amount)`。面额 `[1,3,4]`、金额 `6` 是贪心反例。

## P14 最长递增子序列

`tails[length - 1]` 保存该长度递增子序列的最小末尾值。它不是实际子序列，但足以计算长度。

```python
from bisect import bisect_left


def lis_length(nums: list[int]) -> int:
    tails: list[int] = []
    for x in nums:
        position = bisect_left(tails, x)
        if position == len(tails):
            tails.append(x)
        else:
            tails[position] = x
    return len(tails)


assert lis_length([10, 9, 2, 5, 3, 7, 101, 18]) == 4
assert lis_length([2, 2, 2]) == 1
```

时间 `O(n log n)`，空间 `O(n)`。严格递增使用 `bisect_left`。

## P15 状态占用率

计数后除以序列长度。先验证状态范围，避免负下标悄悄写入错误位置。

```python
def state_occupancy(states: list[int], k: int) -> list[float]:
    counts = [0] * k
    for state in states:
        if not 0 <= state < k:
            raise ValueError("state out of range")
        counts[state] += 1
    if not states:
        return [0.0] * k
    return [count / len(states) for count in counts]


assert state_occupancy([0, 1, 1, 2], 3) == [0.25, 0.5, 0.25]
assert state_occupancy([], 2) == [0.0, 0.0]
```

时间 `O(T + k)`，空间 `O(k)`。

## P16 被试级数据拆分

划分单位是被试，不是 trial。测试被试集合一旦确定，同一人的全部记录都进入测试集。

```python
def split_by_subject(
    records: list[tuple[str, int]], test_subjects: set[str]
) -> tuple[list[tuple[str, int]], list[tuple[str, int]]]:
    train, test = [], []
    for record in records:
        (test if record[0] in test_subjects else train).append(record)
    train_subjects = {subject for subject, _ in train}
    observed_test_subjects = {subject for subject, _ in test}
    if train_subjects & observed_test_subjects:
        raise AssertionError("subject leakage")
    return train, test


records = [("s1", 1), ("s1", 2), ("s2", 1)]
train, test = split_by_subject(records, {"s2"})
assert train == [("s1", 1), ("s1", 2)]
assert test == [("s2", 1)]
```

时间 `O(n)`，输出外空间 `O(s)`。标准化、特征选择和调参也必须只使用训练被试。

## P17-P18 模拟题评分要点

- P17.2 使用拓扑排序并返回完整顺序；不要只返回布尔值。
- P17.3 先统计转移，再逐行归一化；零出边行不能除以零。
- P18.2 递归代码短，但大网格可能超过递归深度；迭代栈更稳妥。
- P18.3 用 `[1,3,4]` 和金额 `6` 说明贪心会选 `4+1+1`，而最优是 `3+3`。
- P18.4 先按被试统计 trial，再在训练集合内确定筛除名单；测试集只应用锁定规则。

模拟结束后只记录三类错误：没有识别算法模式、边界条件遗漏、实现与思路不一致。下一次训练应针对错误类型，而不是随机刷新题。
