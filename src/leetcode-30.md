# leetcode-algorithms-30 Substring with Concatenation of All Words

You are given a string, s, and a list of words, words, that are all of the same length. Find all starting indices of substring(s) in s that is a concatenation of each word in words exactly once and without any intervening characters.

Example 1:
```
Input:
  s = "barfoothefoobarman",
  words = ["foo","bar"]
Output: [0,9]
Explanation: Substrings starting at index 0 and 9 are "barfoor" and "foobar" respectively.
The output order does not matter, returning [9,0] is fine too.
```
Example 2:
```
Input:
  s = "wordgoodstudentgoodword",
  words = ["word","student"]
Output: []
```

## 解法

words里都是相同长度的字符串,由此我们可得到需要匹配的字符串的长度.然后在主串里取出该长度的字条串,到words里去匹配.那该怎么匹配呢,可以把所有的word存到一个map里,计算其出现的次数.在需要匹配的字符串里把每个word取出来,判断是否在map里,如果存在把它也存在另个map1里(这个的目的是出现word重复里要判断出现的次数)然后和map比较,若次数大于就表示不匹配.
```
class Solution {
public:
    vector<int> findSubstring(string s, vector<string>& words)
    {
        std::vector<int> res;
        if (s.size() == 0 || words.size() == 0)
            return res;
        
        //count word 
        std::unordered_map<string, int> stats;
        for (std::string word : words)
            stats[word]++;      
        
        int n = s.size();
        int num = words.size();
        int len = words[0].length();
        for (int i = 0; i < n - num * len + 1; i++)
        {
            std::unordered_map<string, int> subword;
            int j = 0;
            for (; j < num; j++)
            {
                std::string word = s.substr(i + j * len, len);
                if (stats.find(word) != stats.end())
                {
                    subword[word]++;
                    if (subword[word] > stats[word])
                        break;
                }
                else
                    break;
            }
            
            if (j == num)
                res.push_back(i);
        }
        
        return res;
    }
};
```
时间复杂度: O(n * m).n是字条串长度,m是word的个数.

空间复杂度: O(2m).m是word的个数.