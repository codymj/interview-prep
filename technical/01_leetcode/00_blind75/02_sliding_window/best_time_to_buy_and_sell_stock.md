# [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock)

You are given an array `prices` where `prices[i]` is the price of a given stock
on the i<sup>th</sup> day.

You want to maximize your profit by choosing a **single day** to buy one stock
and choosing a **different day in the future** to sell that stock.

Return the *maximum profit you can achieve from this transaction*. If you cannot
achieve any profit, return `0`.

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        // Price we want to buy at and the max profit tracker.
        int buy = prices[0];
        int max_profit{};

        // Iterate over the prices array.
        // If we come across a lower price, set that to the buy price.
        // Otherwise, note profit for that day and replace max profit if needed.
        for (int i=1; i<prices.size(); ++i) {
            if (prices[i] < buy) {
                buy = prices[i];
            } else if (prices[i] - buy > max_profit) {
                max_profit = prices[i] - buy;
            }
        }

        return max_profit;
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over the `prices` vector once.

Space complexity is `O(1)` since we're not allocating any additional memory with
respect to the size of the input.
