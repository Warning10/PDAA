#include <bits/stdc++.h>
using namespace std;

struct item
{
    int id;
    int weight;
    int profit;
    double taken;
};

static bool cmp(item a, item b)
{
    double r1 = (double)a.profit / (double)a.weight;
    double r2 = (double)b.profit / (double)b.weight;
    return r1 > r2;
}

void fractional_knapsack(vector<item> arr, int W)
{

    sort(arr.begin(), arr.end(), cmp);

    double final_profit = 0;

    for (int i = 0; i < arr.size(); i++)
    {
        if (arr[i].weight <= W)
        {
            W = W - arr[i].weight;
            final_profit = final_profit + arr[i].profit;
            arr[i].taken = 1;
        }
        else
        {
            final_profit = final_profit + arr[i].profit * ((double)W / (double)arr[i].weight);
            arr[i].taken = (double)W / (double)arr[i].weight;
            break;
        }
    }

    cout << "Knapsack Contents : " << endl;
    cout << " Item ID : Taken Fraction" << endl;
    int x = 0;
    while (x < arr.size())
    {
        for (auto it : arr)
        {
            if (x == it.id)
            {
                cout << it.id << "\t : \t" << it.taken << endl;
                break;
            }
        }
        x++;
    }
    cout << endl;
    cout << "Final Profit : " << final_profit << endl;
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

    fractional_knapsack(arr, W);
    return 0;
}