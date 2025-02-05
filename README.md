[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/6wGdpkN5)
# 1. Longest Nice Substring
class Solution 
{
public:
string longestNiceSubstring(string s) {
        if (s.size() < 2) return "";
        unordered_set<char> st(begin(s), end(s));
        for (int i = 0; i < s.size(); i++) {
             if (st.find((char) toupper(s[i])) == end(st) || st.find((char) tolower(s[i])) == end(st)) {
                string s1 = longestNiceSubstring(s.substr(0, i));
                string s2 = longestNiceSubstring(s.substr(i + 1));
                return s1.size() >= s2.size() ? s1 : s2;
            }
        }
        return s;
    }
};
# 2. Reverse Bits
class Solution {
public:
    uint32_t reverseBits(uint32_t n) 
    {
        string bits = bitset<32>(n).to_string();
        reverse(bits.begin(), bits.end());

        int ans = stoll(bits, NULL, 2);
        return ans;
    }
};
![image](https://github.com/user-attachments/assets/34ec4029-7345-423f-a577-f4635cb7d5fa)
# 3.Number of 1 Bits
class Solution {
public:
    int hammingWeight(int n) {
        int count = 0;
        for(int i = 31; i >= 0; i--){
            if(((n >> i) & 1) == 1)
                count++;
        }
        return count;
    }
};
![image](https://github.com/user-attachments/assets/1cfcb68c-a242-4d3e-8fbe-424bbb271035)
# 4.Max subarrays
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int n = size(nums), ans = INT_MIN;
        for(int i = 0; i < n; i++) 
            for(int j = i, curSum = 0; j < n ; j++) 
                curSum += nums[j],
                ans = max(ans, curSum);        
        return ans;
    }
};
![image](https://github.com/user-attachments/assets/a7596d07-ed18-4bcc-9216-425a94acd68f)
# 5. Search a2D Matrix
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int n = matrix.size(), m = matrix[0].size();
        int row = 0, col = m - 1; 

        while (row < n && col >= 0) {
            if (matrix[row][col] == target) return true;
            else if (matrix[row][col] < target) row++; 
            else col--;
        }
        return false;
    }
};
![image](https://github.com/user-attachments/assets/bd571ddd-9eee-477c-aa54-04f1f98be12c)
# 6.Super Power
class Solution {
    const int base = 1337;
    int powmod(int a, int k) //a^k mod 1337 where 0 <= k <= 10
    {
        a %= base;
        int result = 1;
        for (int i = 0; i < k; ++i)
            result = (result * a) % base;
        return result;
    }
public:
    int superPow(int a, vector<int>& b) {
        if (b.empty()) return 1;
        int last_digit = b.back();
        b.pop_back();
        return powmod(superPow(a, b), 10) * powmod(a, last_digit) % base;
    }
};
![image](https://github.com/user-attachments/assets/b733c8cf-50a1-4679-9033-b859f30a5bae)
# 7.Beautiful Array
class Solution {
public:
    vector<int> beautifulArray(int n) {
        if(n==1)
            return {1};
        vector<int> even = beautifulArray(n/2);
        vector<int> odd = beautifulArray(n-(n/2));
        vector<int>ans;
        for(auto e:even)
            ans.push_back(2*e);
        for(auto e:odd)
            ans.push_back((2*e)-1);
        return ans;
    }
};
![image](https://github.com/user-attachments/assets/49a2a3c1-970a-4dc7-95a2-e62f3ac35a9a)






# 8.The Skyline Problem
class Solution {
public:
    vector<vector<int>> getSkyline(vector<vector<int>>& buildings) {
        vector<pair<int, int>> events;
        priority_queue<int> heights;
        vector<vector<int>> result;
        
        // Collect start and end points of buildings
        for (const auto& b : buildings) {
            events.emplace_back(b[0], -b[2]); // Start event (negative height to differentiate)
            events.emplace_back(b[1], b[2]);  // End event (positive height)
        }
        
        // Sort events: first by x, then by height (start events before end events)
        sort(events.begin(), events.end());

        heights.push(0); // Sentinel value for ground level
        int prevHeight = 0;
        
        for (const auto& [x, h] : events) {
            if (h < 0) {
                heights.push(-h); // Add new building height
            } else {
                // Remove the height (inefficient but simple approach)
                vector<int> temp;
                while (!heights.empty() && heights.top() != h) {
                    temp.push_back(heights.top());
                    heights.pop();
                }
                if (!heights.empty()) heights.pop(); // Remove the matched height
                for (int th : temp) heights.push(th); // Restore other heights
            }
            
            int currHeight = heights.top();
            if (currHeight != prevHeight) { // Only add to result if height changes
                result.push_back({x, currHeight});
                prevHeight = currHeight;
            }
        }
        
        return result;
    }
};
![image](https://github.com/user-attachments/assets/c9f28496-1a7c-4ace-94a6-f7902fe7e754)
# Reverse Pairs
class Solution {
public:
    int reversePairs(vector<int>& nums) {
        int n = nums.size();
        long long reversePairsCount = 0;
        for(int i=0; i<n-1; i++){
            for(int j=i+1; j<n; j++){
                if(nums[i] > 2*(long long)nums[j]){
                    reversePairsCount++;
                }
            }
        }
        return reversePairsCount;
    }
};
![image](https://github.com/user-attachments/assets/08df894a-e076-48bd-bce1-9a1312746f87)
# 10.Longest increasing Sunsequence
class MaxSegmentTree {
 public:
  int n;
  vector<int> tree;
  MaxSegmentTree(int n_) : n(n_) {
    int size = (int)(ceil(log2(n)));
    size = (2 * pow(2, size)) - 1;
    tree = vector<int>(size);
  }
  
  int max_value() { return tree[0]; }

  int query(int l, int r) { return query_util(0, l, r, 0, n - 1); }

  int query_util(int i, int qL, int qR, int l, int r) {
    if (l >= qL && r <= qR) return tree[i];
    if (l > qR || r < qL) return INT_MIN;

    int m = (l + r) / 2;
    return max(query_util(2 * i + 1, qL, qR, l, m), query_util(2 * i + 2, qL, qR, m + 1, r));
  }

  void update(int i, int val) { update_util(0, 0, n - 1, i, val); }
  void update_util(int i, int l, int r, int pos, int val) {
    if (pos < l || pos > r) return;
    if (l == r) {
      tree[i] = max(val, tree[i]);
      return;
    }

    int m = (l + r) / 2;
    update_util(2 * i + 1, l, m, pos, val);
    update_util(2 * i + 2, m + 1, r, pos, val);
    tree[i] = max(tree[2 * i + 1], tree[2 * i + 2]);
  }
};

class Solution {
 public:
  int lengthOfLIS(vector<int>& nums, int k) {
    MaxSegmentTree tree(1e5 + 1);
    for (int i : nums) {
      int lower = max(0, i - k);
      int cur = 1 + tree.query(lower, i - 1);
      tree.update(i, cur);
    }

    return tree.max_value();
  }
};
![image](https://github.com/user-attachments/assets/818a3b1d-6162-4a30-b402-74cc82a66ddb)


