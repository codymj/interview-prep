# [39. Combination Sum](https://leetcode.com/problems/combination-sum)

Given an array of **distinct** integers `candidates` and a target integer
`target`, return *a list of all **unique combinations** of* `candidates` *where
the chosen numbers sum to* `target`. You may return the combinations in **any
order**.

The same number may be chosen from `candidates` an **unlimited number of
times**. Two combinations are unique if the frequency of at least one of the
chosen numbers is different.

The test cases are generated such that the number of unique combinations that
sum up to `target` is less than `150` combinations for the given input.

Constraints:

* `1 <= candidates.length <= 30`
* `2 <= candidates[i] <= 40`
* All elements of `candidates` are distinct.
* `1 <= target <= 40`

## Solution

```c++
class Solution {
private:
    std::vector<std::vector<int>> m_ans{};
    std::vector<int> m_tmp{};
    std::vector<int>* m_candidates{};

public:
    std::vector<std::vector<int>> combinationSum(std::vector<int>& candidates, int target) {
        // Initialize.
        // Sort candidates so we can break out early in backtracking stage.
        std::sort(candidates.begin(), candidates.end());
        m_candidates = &candidates;

        // Begin recursion.
        backtrack(0, target);

        return m_ans;
    }

    void backtrack(int idx, int target) {
        // Target is 0, so we found a group of candidates.
        // Add the temporary list to our answer list.
        if (target == 0) {
            m_ans.push_back(m_tmp);
            return;
        }

        // Search for candidates.
        // No need to continue searching if candidate is greater than target.
        for (int i=idx; i<m_candidates->size(); ++i) {
            if ((*m_candidates)[i] > target) {
                break;
            }
            m_tmp.push_back((*m_candidates)[i]);
            backtrack(i, target - (*m_candidates)[i]);
            m_tmp.pop_back();
        }
    }
};

```

## Analysis

Time complexity is `O(n^(target/c_min))` where `n` is number of candidates and
`c_min` is the smallest candidate which determines the maximum depth of the
decision tree. Since we're sorting and pruning, it should help with efficiency.

Space complexity is going to be `O(n^(target/c_min))` as well since the temp
storage is dependent on decision tree depth.
