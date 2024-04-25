#include <bits/stdc++.h>
using namespace std;

void printSolution(const vector<vector<int>> &board, int x, int y, int N)
{
    cout << "N Queen Backtracking Solution:" << endl;
    cout << "Given initial position of 1st queen at row: " << x << " column: " << y << endl;
    for (const auto &line : board)
    {
        for (int cell : line)
        {
            cout << cell << " ";
        }
        cout << endl;
    }
}

bool solveNQUtil(vector<vector<int>> &board, vector<int> &ld, vector<int> &rd,
                 vector<int> &cl, int col, int x, int y, int N)
{
    if (col >= N)
    {
        return true;
    }
    if (col == y)
    {
        return solveNQUtil(board, ld, rd, cl, col + 1, x, y, N);
    }
    for (int i = 0; i < N; i++)
    {
        if (i == x)
        {
            continue;
        }
        if (ld[i - col + N - 1] != 1 && rd[i + col] != 1 && cl[i] != 1)
        {
            board[i][col] = 1;
            ld[i - col + N - 1] = rd[i + col] = cl[i] = 1;
            if (solveNQUtil(board, ld, rd, cl, col + 1, x, y, N))
            {
                return true;
            }
            board[i][col] = 0;
            ld[i - col + N - 1] = rd[i + col] = cl[i] = 0;
        }
    }
    return false;
}

bool solveNQ(int x, int y, int N)
{
    vector<vector<int>> board(N, vector<int>(N, 0));
    vector<int> ld(2 * N - 1, 0);
    vector<int> rd(2 * N - 1, 0);
    vector<int> cl(N, 0);

    board[x][y] = 1;
    ld[x - y + N - 1] = rd[x + y] = cl[x] = 1;

    if (!solveNQUtil(board, ld, rd, cl, 0, x, y, N))
    {
        cout << "Solution does not exist" << endl;
        return false;
    }
    printSolution(board, x, y, N);
    return true;
}

int main()
{
    cout << "Enter Size of Chess board: ";
    int N;
    cin >> N;
    cout << "For the first queen - " << endl;
    int x, y;
    cin >> x >> y;
    solveNQ(x, y, N);
    return 0;
}
