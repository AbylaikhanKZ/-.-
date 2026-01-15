#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    ios_base::sync_with_stdio(false); 
    cin.tie(nullptr);
    int n;
    cin >> n;
    vector <pair <long long, int>> ind(n + 1);
    ind[0] = {0, 0};
    vector <long long> a(n + 1, 0); 
    for (int i = 0; i < n; i++) {
        long long temp;
        cin >> temp;
        a[i + 1] = a[i] + temp;
        ind[i + 1].first = a[i + 1];
        ind[i + 1].second = i + 1;
    }
    sort(ind.begin(), ind.end());
    int ans1, ans2;
    for (int i = 0; i < n; i++) {
        if (ind[i].first == ind[i + 1].first) {
            ans1 = min(ind[i].second, ind[i + 1].second);
            ans2 = max(ind[i].second, ind[i + 1].second);
            break;
        }
    }
    cout << ans1 << " " << ans2;
    return 0;
}
// Найти сумму полупрямоугольник с префиксными суммами 
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, m;
    cin >> n >> m;

    vector<vector<long long>> a(n + 1, vector<long long>(m + 1, 0));
    vector<vector<long long>> p(n + 1, vector<long long>(m + 1, 0));

    // Чтение массива (с 1-индексацией)
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            cin >> a[i][j];
        }
    }

    // Построение 2D-префиксов по формуле
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            p[i][j] = a[i][j]
                    + p[i-1][j]
                    + p[i][j-1]
                    - p[i-1][j-1];
        }
    }

    int q;
    cin >> q;

    while (q--) {
        int lx, ly, rx, ry;
        cin >> lx >> ly >> rx >> ry;

        long long ans =
              p[rx][ry]
            - p[lx-1][ry]
            - p[rx][ly-1]
            + p[lx-1][ly-1];

        cout << ans << '\n';
    }

    return 0;
}
