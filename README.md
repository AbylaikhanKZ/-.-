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
