 Longest Repeating Character Replacement : https://leetcode.com/problems/longest-repeating-character-replacement/description/
explanation :-
int n = s.length();
        int[] freq = new int[26];
        int left = 0;
        int maxFreq = 0;
        int res = 0;
        for (int right = 0; right < n; right++) {
            int idx = s.charAt(right) - 'A';
            freq[idx]++;
            // keep track of maximum frequency in window
            maxFreq = Math.max(maxFreq, freq[idx]);
            int windowLen = right - left + 1;
            // if replacements needed > k, shrink window
            if (windowLen - maxFreq > k) {
                freq[s.charAt(left) - 'A']--;
                left++;
            }
            res = Math.max(res, right - left + 1);
        }
        return res;


explain this code visually

![Alt text](E:\Develoupment\Daily_DSA\Pattern 2_Sliding_Window\explain.png)   

Show less
4:55 PM
I'll explain this Longest Repeating Character Replacement algorithm visually!

Problem:
Find the longest substring where you can make all characters the same by changing at most k characters.

Visual Walkthrough
Input: s = "AABABBA", k = 1

Key Insight:
windowLength - maxFrequency = replacements needed

If replacements needed > k → window is invalid, shrink it!
Step-by-Step Execution:
Initial: freq[] = [0,0,0,...], left=0, maxFreq=0, res=0
right = 0: 'A'
Window: [A]
        ↑
      left,right

freq[A] = 1
maxFreq = 1 (most frequent char count)
windowLen = 1
replacements needed = 1 - 1 = 0 ≤ k ✅ Valid!
res = 1
right = 1: 'A'
Window: [A A]
        ↑   ↑
      left right

freq[A] = 2
maxFreq = 2
windowLen = 2
replacements = 2 - 2 = 0 ≤ k ✅ Valid!
res = 2
right = 2: 'B'
Window: [A A B]
        ↑     ↑
      left  right

freq[A]=2, freq[B]=1
maxFreq = 2 (still A)
windowLen = 3
replacements = 3 - 2 = 1 ≤ k ✅ Valid!
res = 3

Meaning: "AAB" → can change B to A with 1 replacement → "AAA"
right = 3: 'A'
Window: [A A B A]
        ↑       ↑
      left    right

freq[A]=3, freq[B]=1
maxFreq = 3
windowLen = 4
replacements = 4 - 3 = 1 ≤ k ✅ Valid!
res = 4

"AABA" → change B to A → "AAAA"
right = 4: 'B'
Window: [A A B A B]
        ↑         ↑
      left      right

freq[A]=3, freq[B]=2
maxFreq = 3
windowLen = 5
replacements = 5 - 3 = 2 > k ❌ INVALID!

Need 2 replacements but k=1!
→ SHRINK WINDOW
Shrinking:

freq[s.charAt(left) - 'A']--;  // freq[A]--
left++;

Window: [A B A B]
          ↑     ↑
        left  right

freq[A]=2, freq[B]=2
windowLen = 4
replacements = 4 - 2 = 2 > k still... but we don't shrink again
(algorithm only checks once per expansion)
res stays 4
right = 5: 'B'
Window: [A B A B B]
          ↑       ↑
        left    right

freq[A]=2, freq[B]=3
maxFreq = 3
windowLen = 5
replacements = 5 - 3 = 2 > k ❌ SHRINK!

After shrink:
Window: [B A B B]
            ↑   ↑
          left right
res = 4
right = 6: 'A'
Window: [B A B B A]
            ↑     ↑
          left  right

freq[A]=2, freq[B]=3
maxFreq = 3
windowLen = 5
replacements = 5 - 3 = 2 > k ❌ SHRINK!

After shrink:
Window: [A B B A]
              ↑ ↑
            left right
res = 4
Final Answer: 4
Best substring: "AABA" → replace 1 B → "AAAA"

Visual Summary:
The algorithm maintains a sliding window:

Valid window (replacements ≤ k):
[A A A B]  ← maxFreq=3, need 1 replacement ✅
 ↑     ↑

Invalid window (replacements > k):
[A A B A B]  ← maxFreq=3, need 2 replacements ❌
 ↑       ↑
 Shrink left pointer →
Time: O(n) - single pass
Space: O(1) - fixed array of size 26



