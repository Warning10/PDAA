#include <bits/stdc++.h>
using namespace std;

int partition(vector<int> &arr, int low, int high)
{
    int pivot = low;
    int left = low;
    int right = high;

    while (left < right)
    {
        while (arr[left] <= arr[pivot] && left <= high)
            left++;
        while (arr[right] > arr[pivot] && right >= low)
            right--;
        if (left < right)
            swap(arr[left], arr[right]);
    }
    swap(arr[pivot], arr[right]);
    return right;
}

void deterministic_quick_sort(vector<int> &arr, int low, int high)
{
    if (low < high)
    {
        int pi = partition(arr, low, high);
        deterministic_quick_sort(arr, low, pi - 1);
        deterministic_quick_sort(arr, pi + 1, high);
    }
}

int randomized_partition(vector<int> &arr, int low, int high)
{
    int random = low + rand() % (high - low);
    swap(arr[random], arr[high]);
    return partition(arr, low, high);
}

void randomized_quick_sort(vector<int> &arr, int low, int high)
{
    if (low < high)
    {
        int pi = randomized_partition(arr, low, high);
        randomized_quick_sort(arr, low, pi - 1);
        randomized_quick_sort(arr, pi + 1, high);
    }
}

int main()
{
    int n;
    cout << "Enter the size of array : ";
    cin >> n;

    vector<int> arr1;
    vector<int> arr2;

    cout << "Enter the elements : " << endl;
    for (int i = 0; i < n; i++)
    {
        int ele;
        cin >> ele;
        arr1.push_back(ele);
        arr2.push_back(ele);
    }

    deterministic_quick_sort(arr1, 0, arr1.size() - 1);

    cout << "Deterministic Quick Sort : " << endl;
    for (auto i : arr1)
    {
        cout << i << " ";
    }
    cout << endl
         << endl;

    randomized_quick_sort(arr2, 0, arr2.size() - 1);

    cout << "Randomized Quick Sort : " << endl;
    for (auto i : arr2)
    {
        cout << i << " ";
    }

    return 0;
}