### Longest Repeating Character Replacement
- 这种需要一段一段连续元素比较的就是用滑动窗口
- count[26]保存每个字母的个数
- start end 都设置为0，end逐渐+1
- end++后检测新字母的个数是否能当上maxCount
- 现在`滑动窗口长度 - maxcount > k`的话，证明start需要收缩了,start--
- 最后检测当前滑动窗口长度是否能当上maxLength

```
class Solution {
    public int characterReplacement(String s, int k) {
        int[] count = new int[26];
        int maxCount = 0;
        int maxLength = 0;
        int start = 0;
        for (int end = 0; end < s.length(); end++){
            //
            count[s.charAt(end)-'A']++;
            maxCount = Math.max(maxCount, count[s.charAt(end)-'A']);
            //
            while (end - start + 1 - maxCount > k){
                count[s.charAt(start) - 'A']--;
                start++;
            }
            maxLength = Math.max(maxLength, end - start + 1);
        }
        return maxLength;
    }
}
```
