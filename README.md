# 1625-lexiographically-smallest-string-after-applying-operations
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    string findLexSmallestString(string s, int a, int b) {
        string ans = s;
        unordered_set<string> seen;
        queue<string> q;
        q.push(s);
        seen.insert(s);
        while (!q.empty()) {
            string cur = q.front();
            q.pop();
            if (cur < ans) ans = cur;
            string t1 = cur;
            for (int i = 1; i < (int)t1.size(); i += 2) {
                int digit = t1[i] - '0';
                digit = (digit + a) % 10;
                t1[i] = char('0' + digit);
            }
            if (seen.insert(t1).second) q.push(t1);
            string t2 = cur.substr(cur.size() - b) + cur.substr(0, cur.size() - b);
            if (seen.insert(t2).second) q.push(t2);
        }
        return ans;
    }
};
