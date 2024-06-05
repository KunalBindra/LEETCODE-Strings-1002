# LEETCODE-Strings-1002
Sure, let's perform a dry run of the provided code with an example input to understand how it works step by step.

Let's use the example input: `["bella", "label", "roller"]`.

Here's the code for reference:
```java
class Solution {
  public List<String> commonChars(String[] A) {
    List<String> ans = new ArrayList<>();
    int[] commonCount = new int[26];
    Arrays.fill(commonCount, Integer.MAX_VALUE);

    for (String a : A) {
      int[] count = new int[26];
      for (char c : a.toCharArray())
        ++count[c - 'a'];
      for (int i = 0; i < 26; ++i)
        commonCount[i] = Math.min(commonCount[i], count[i]);
    }

    for (char c = 'a'; c <= 'z'; ++c)
      for (int i = 0; i < commonCount[c - 'a']; ++i)
        ans.add(String.valueOf(c));

    return ans;
  }
}
```

### Initial State
- `commonCount`: An array of size 26 (for each letter of the alphabet) filled with `Integer.MAX_VALUE`.

### Iteration 1: Processing "bella"
1. Initialize `count` to all zeros.
2. For each character in "bella":
   - 'b' -> `count['b' - 'a']++` -> `count[1] = 1`
   - 'e' -> `count['e' - 'a']++` -> `count[4] = 1`
   - 'l' -> `count['l' - 'a']++` -> `count[11] = 1`
   - 'l' -> `count['l' - 'a']++` -> `count[11] = 2`
   - 'a' -> `count['a' - 'a']++` -> `count[0] = 1`
3. Update `commonCount` with minimum values:
   - `commonCount[i] = Math.min(commonCount[i], count[i])` for each i:
     - commonCount[0] = min(Integer.MAX_VALUE, 1) = 1
     - commonCount[1] = min(Integer.MAX_VALUE, 1) = 1
     - commonCount[4] = min(Integer.MAX_VALUE, 1) = 1
     - commonCount[11] = min(Integer.MAX_VALUE, 2) = 2

Resulting `commonCount` after "bella":
```
commonCount = [1, 1, Integer.MAX_VALUE, Integer.MAX_VALUE, 1, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, 2, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE]
```

### Iteration 2: Processing "label"
1. Initialize `count` to all zeros.
2. For each character in "label":
   - 'l' -> `count['l' - 'a']++` -> `count[11] = 1`
   - 'a' -> `count['a' - 'a']++` -> `count[0] = 1`
   - 'b' -> `count['b' - 'a']++` -> `count[1] = 1`
   - 'e' -> `count['e' - 'a']++` -> `count[4] = 1`
   - 'l' -> `count['l' - 'a']++` -> `count[11] = 2`
3. Update `commonCount` with minimum values:
   - `commonCount[i] = Math.min(commonCount[i], count[i])` for each i:
     - commonCount[0] = min(1, 1) = 1
     - commonCount[1] = min(1, 1) = 1
     - commonCount[4] = min(1, 1) = 1
     - commonCount[11] = min(2, 2) = 2

Resulting `commonCount` after "label":
```
commonCount = [1, 1, Integer.MAX_VALUE, Integer.MAX_VALUE, 1, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, 2, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE]
```

### Iteration 3: Processing "roller"
1. Initialize `count` to all zeros.
2. For each character in "roller":
   - 'r' -> `count['r' - 'a']++` -> `count[17] = 1`
   - 'o' -> `count['o' - 'a']++` -> `count[14] = 1`
   - 'l' -> `count['l' - 'a']++` -> `count[11] = 1`
   - 'l' -> `count['l' - 'a']++` -> `count[11] = 2`
   - 'e' -> `count['e' - 'a']++` -> `count[4] = 1`
3. Update `commonCount` with minimum values:
   - `commonCount[i] = Math.min(commonCount[i], count[i])` for each i:
     - commonCount[0] = min(1, 0) = 0
     - commonCount[1] = min(1, 0) = 0
     - commonCount[4] = min(1, 1) = 1
     - commonCount[11] = min(2, 2) = 2

Resulting `commonCount` after "roller":
```
commonCount = [0, 0, Integer.MAX_VALUE, Integer.MAX_VALUE, 1, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, 2, Integer.MAX_VALUE, Integer.MAX_VALUE, 0, Integer.MAX_VALUE, Integer.MAX_VALUE, 0, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE, Integer.MAX_VALUE]
```

### Constructing the Result List
- Iterate from 'a' to 'z':
  - For 'e': commonCount[4] = 1 -> add 'e' to the result list.
  - For 'l': commonCount[11] = 2 -> add 'l' twice to the result list.

Final result list:
```
ans = ["e", "l", "l"]
```

So the method `commonChars` correctly returns the common characters in all strings, which is `["e", "l", "l"]` for the input `["bella", "label", "roller"]`.
