#include <bits/stdc++.h>
using namespace std;

map<char, string> code_map;

struct node
{
    char ch;
    int freq;

    node *left;
    node *right;

    node(char c, int f)
    {
        this->left = NULL;
        this->right = NULL;
        this->ch = c;
        this->freq = f;
    }
};

struct compare
{
    bool operator()(node *l, node *r)
    {
        return (l->freq > r->freq);
    }
};

void print_codes(node *root, string str)
{
    if (!root)
        return;

    if (32 <= root->ch && root->ch <= 126)
    {
        cout << root->ch << " : " << str << "\n";
        code_map[root->ch] = str;
    }

    print_codes(root->left, str + "0");
    print_codes(root->right, str + "1");
}

void huffman_codes(vector<char> char_arr, vector<int> freq_arr)
{
    priority_queue<node *, vector<node *>, compare> min_heap;

    for (int i = 0; i < char_arr.size(); i++)
    {
        min_heap.push(new node(char_arr[i], freq_arr[i]));
    }

    while (min_heap.size() > 1)
    {
        node *left = min_heap.top();
        min_heap.pop();

        node *right = min_heap.top();
        min_heap.pop();

        node *top = new node((char)0, left->freq + right->freq);
        top->left = left;
        top->right = right;

        min_heap.push(top);
    }

    print_codes(min_heap.top(), "");
}

int main()
{
    map<char, int> mp;
    string input;

    ifstream fin;
    fin.open("input.txt");

    while (!fin.eof())
    {
        char ch;
        fin >> std::noskipws >> ch;
        input += ch;
        mp[ch]++;
    }

    vector<char> char_arr;
    vector<int> freq_arr;

    for (auto it : mp)
    {
        char_arr.push_back(it.first);
        freq_arr.push_back(it.second);
    }

    huffman_codes(char_arr, freq_arr);

    return 0;
}