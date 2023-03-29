```python
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        dict = {}
        substr = ""
        maxlen = 0
        for i in range(0,len(s)):
            if dict.get(s[i],-1) == -1: # 사전에 정의되지 않았다면
                dict[s[i]] = i # 사전에 정의
                substr += s[i]
                if maxlen < len(substr):
                        maxlen = len(substr)
            else: # 사전에 정의되어 있다면
                if s[i] == s[i-1]: # 바로전 단어와 같을 경우 pwwkew / 현재는 pw[w]
                    substr = "" # "pw" -> ""
                    substr += s[i] # "" -> "w"
                else: # 바로전 단어와 다를 경우 => dvdf, ckilbkd, abba
                    if s[i] not in substr:
                        substr += s[i]
                        # 해당 조건문을 지우고 dict를 비우는 방법 구색중
                        # dict.clear()
                        # dict[s[i]] = i
                    else:
                        idx = substr.index(s[i]) # 현재 단어의 인덱스를 구해서
                        substr = substr[idx+1:] # 그 인덱스의 왼쪽을 전부 짜름 
                        substr += s[i] # 다시 해당하는 단어 +
            if maxlen < len(substr):
                maxlen = len(substr)

        return maxlen

```

## Feedback
---
### 상우
1. 조건문을 잘 활용한 만큼 조금 더 간단한 조건문 처리를 한다면 더 좋은 코드가 될 수 있을 것으로 보임
2. 단어를 자르면서 구분한 것이 인상적임
---
### 좌오
