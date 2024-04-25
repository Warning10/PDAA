#include <bits/stdc++.h>
using namespace std;

struct item
{
    int id;
    int weight;
    int profit;
    double taken;
};

int knapsack(vector<item> arr, int W)
{
    int dp[W + 1];
    memset(dp, 0, sizeof(dp));

    for (int i = 1; i < arr.size() + 1; i++)
    {
        for (int w = W; w >= 0; w--)
        {
            if (arr[i - 1].weight <= w)
            {
                dp[w] = max(dp[w], dp[w - arr[i - 1].weight] + arr[i - 1].profit);
            }
        }
    }

    return dp[W];
}

int main()
{
    int W;
    cout << "Enter the capacity of knapsack : ";
    cin >> W;

    int n;
    cout << "Enter the no. items : ";
    cin >> n;

    vector<item> arr(n);

    for (int i = 0; i < n; i++)
    {
        item it;
        int id, w, p, tk;
        cout << "Enter weight and profit of item " << i << " : " << endl;
        cin >> w;
        cin >> p;

        it.id = i;
        it.weight = w;
        it.profit = p;
        it.taken = 0.0;

        arr.push_back(it);
    }

    int final_profit = knapsack(arr, W);
    cout << "Final Profit : " << final_profit << endl;

    return 0;
}