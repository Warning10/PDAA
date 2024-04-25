#include <bits/stdc++.h>
#include <iostream>

using namespace std;

int fibonacci_recursive(int n)
{
    if (n <= 1)
        return n;
    return fibonacci_recursive(n - 1) + fibonacci_recursive(n - 2);
}

int fibonacci_iterative(int n)
{
    int a = 0;
    int b = 1;
    if (n == 1)
        return a;
    if (n == 2)
        return b;
    int c;
    int loop = n - 2;
    do
    {
        c = a + b;
        a = b;
        b = c;
    } while (loop--);

    return c;
}

int main()
{
    int n;
    cout << "Enter n : " << endl;
    cin >> n;
    cout << "n'th fibonacci no. with iterative method : " << fibonacci_iterative(n) << endl;
    cout << "n'th fibonacci no. with recursive method : " << fibonacci_recursive(n) << endl;

    return 0;
}