Priority 1: Strings + Hashing + Stack
Questions:
1. Valid Parentheses
2. Reverse Words in a String
3. Valid Anagram
4. Reverse String
5. Longest Substring Without Repeating Characters
6. Group Anagrams
Resources:
- LeetCode — Stack problems
- LeetCode — Sliding Window problems
  
Priority 2: Arrays + Two Pointers + Sliding Window
Reported array rotation aur sliding-window maximum ko dekhte hue yeh group important hai.

Questions:
1. Rotate Array
2. Sliding Window Maximum
3. Two Sum
4. Maximum Subarray
5. Move Zeroes
6. Best Time to Buy and Sell Stock
Resources:
- LeetCode — Array problems
- LeetCode 239 — Sliding Window Maximum

  
Priority 3: Linked List + Queue
Questions:
1. Reverse Linked List
2. Detect Cycle in Linked List
3. Implement Queue using Linked List
4. Circular Linked List
5. Merge Two Sorted Lists
Resources:
- LeetCode — Linked List problems
- GeeksforGeeks — Queue using Linked List

  
Priority 4: Trees + BFS
Ek candidate ne explicitly tree-based BFS report kiya tha.

Questions:
1. Binary Tree Level Order Traversal
2. Maximum Depth of Binary Tree
3. Binary Tree Right Side View
4. Binary Tree Zigzag Level Order Traversal
Resources:
- LeetCode 102 — Binary Tree Level Order Traversal
- LeetCode — Tree problems

  
Priority 5: Prefix Sum + DP
Yahan do reported patterns relevant hain: Longest Subarray with Zero Sum aur Knapsack.

Questions:
1. Longest Subarray with Zero Sum
2. Subarray Sum Equals K
3. 0/1 Knapsack
4. Climbing Stairs
5. House Robber
Resources:
- LeetCode 560 — Subarray Sum Equals K
- GeeksforGeeks — 0/1 Knapsack




1. Valid Parentheses
```
https://leetcode.com/problems/valid-parentheses/description/
```

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> st = new Stack<>();

        for(Character ch : s.toCharArray()){
            if(ch=='('){
                st.push(')');
            }else if(ch=='{'){
                st.push('}');
            }else if(ch=='['){
                st.push(']');
            }else{
                if(st.isEmpty()|| st.pop()!=ch){
                    return false;
                }
            }
        }
        return st.isEmpty();
        
    }
}
```


2.	Reverse Words in a String
```
https://leetcode.com/problems/reverse-words-in-a-string/description/
https://takeuforward.org/practice/dsa/reverse-every-word-in-a-string
```

```java
class Solution {
    public String reverseWords(String s) {
        String[] words = s.trim().split("\\s+");

        StringBuilder ans = new StringBuilder();

        for (int i = words.length - 1; i >= 0; i--) {
            ans.append(words[i]);

            if (i > 0) {
                ans.append(" ");
            }
        }

        return ans.toString();
    }
}
Time Complexity: O(n) (where n is the length of the input string)
Space Complexity: O(n)
```

```java
class Solution {
    public String reverseWords(String s) {
        int n = s.length();

        StringBuilder sb = new StringBuilder(s);
        reverseString(sb, 0, n-1);

        int i=0, j=0, start=0, end=0;
        while(j<n){
            //skip spaces

            while(j<n && sb.charAt(j) == ' ')j++;

            if(j==n) break;

            start = i;

            //copy the word characters forward
            while( j < n && sb.charAt(j)!=' '){
                sb.setCharAt(i++, sb.charAt(j++));
            }

            end = i - 1;

            //reverse the current word using start and end
            reverseString(sb, start, end);

            //add a space after the word if its not the last word
            if(j<n){
                //if(i<sb.length()){
                    sb.setCharAt(i++, ' ');
                //}
            }
        }

        //remove trailing whitespace if present
        if(i > 0 && sb.charAt(i-1) == ' ')i--;

        return sb.substring(0,i);
    }

    private void reverseString(StringBuilder s, int start, int end){
        while(start < end){
            char temp = s.charAt(start);
            s.setCharAt(start, s.charAt(end));
            s.setCharAt(end, temp);
            start++;
            end--;
        }
    }
}
```

```java

class Solution {
    // Function to reverse every word in the given string
    public String reverseWords(String s) {
        int n = s.length(); // Length of string
        
        // List to store the words present in string
        List<String> words = new ArrayList<>();
        
        // Pointers to mark the start and end of a word
        int start, end;
        
        int i = 0;
        while (i < n) {
            
            // Finding the first character of a word (if any)
            while (i < n && s.charAt(i) == ' ') i++;
            
            // If no word is found, break 
            if (i >= n) break;
            
            start = i; // Storing the index of first character of word
            
            // Finding the last character of the word
            while (i < n && s.charAt(i) != ' ') i++;
            
            end = i - 1; // Storing the index of last character of word
            
            // Add the found word to the list of words
            String wordFound = s.substring(start, end + 1);
            words.add(wordFound);
        }
        
        StringBuilder ans = new StringBuilder();
        
        // Adding all the words to result in the reverse order 
        for (int j = words.size() - 1; j >= 0; j--) {
            ans.append(words.get(j));
            
            // Adding spaces in between words
            if (j != 0) ans.append(' ');
        }
        
        return ans.toString(); // Return the stored result
    }
}
Time Complexity: O(n) (where n is the length of the input string)
Space Complexity: O(n)
```
```java
class Solution {
    private void reverseString(StringBuilder s, int start, int end) {
        while (start < end) {
            char temp = s.charAt(start);
            s.setCharAt(start, s.charAt(end));
            s.setCharAt(end, temp);
            start++;
            end--;
        }
    }
 
    public String reverseWords(String s) {
        int n = s.length();
 
        // Reverse the entire string
        StringBuilder sb = new StringBuilder(s);
        reverseString(sb, 0, n - 1);
 
        int i = 0, j = 0, start = 0, end = 0;
 
        while (j < n) {
            // Skip spaces
            while (j < n && sb.charAt(j) == ' ') j++;
            if (j == n) break;
 
            start = i;
 
            // Copy the word characters forward
            while (j < n && sb.charAt(j) != ' ') {
                if (i < sb.length()) {
                    sb.setCharAt(i++, sb.charAt(j++));
                } else {
                    sb.append(sb.charAt(j++));
                    i++;
                }
            }
 
            end = i - 1;
 
            // Reverse the current word using start and end
            reverseString(sb, start, end);
 
            // Add a space after the word if it's not the last word
            if (j < n) {
                if (i < sb.length()) {
                    sb.setCharAt(i++, ' ');
                } else {
                    sb.append(' ');
                    i++;
                }
            }
        }
 
        // Remove trailing space if present
        if (i > 0 && sb.charAt(i - 1) == ' ') i--;
 
        return sb.substring(0, i);
    }
}
Time Complexity: O(n) (where n is the length of the input string)
Space Complexity: O(1)
```


3.	Valid Anagram
```
https://takeuforward.org/practice/dsa/valid-anagram
https://leetcode.com/problems/valid-anagram/
```

```java
public boolean anagramStrings(String s, String t) {
        // If lengths are not equal, they cannot be anagrams
        if (s.length() != t.length()) return false;
 
        // Convert strings to char arrays and sort them
        char[] sArray = s.toCharArray();
        char[] tArray = t.toCharArray();
        Arrays.sort(sArray);
        Arrays.sort(tArray);
 
        // Compare sorted arrays
        return Arrays.equals(sArray, tArray);
    }

 Time Complexity: O(N log N)   
 Space Complexity: O(1)
```


```java
class Solution {
    public boolean isAnagram(String s, String t) {
       if(s.length() !=t.length()) return false;
        int freq[] = new int[26];

        for(int i = 0;i<s.length();i++){
            freq[s.charAt(i)-'a']++;
            freq[t.charAt(i)-'a']--;
        }

        for(int i=0;i<26;i++){
            if(freq[i]!=0){
                return false;
            } 
        }
        
        return true;
    }
}
Time Complexity: O(N)   
Space Complexity: O(1)
```

4.	Reverse String
```
https://leetcode.com/problems/reverse-string/description/
```

```java
1. Approach 1: Two Pointers + Swap Method
class Solution {
    public void reverseString(char[] s) {
        int left = 0, right = s.length - 1;

        while(left < right){
            swap(s, left++, right--);
        }
    }

    private void swap(char[] s, int left, int right){
        char ch = s[left];
        s[left] = s[right];
        s[right] = ch;
    }
}
```
```java
2. Approach 2: Swap Without a Separate Method
class Solution {
    public void reverseString(char[] s) {
        int l = 0, r = s.length -1;
        while(l<r){
            char ch = s[l];
            s[l] = s[r];
            s[r] = ch;
            l++;
            r--;
        }
        
    }
}
```
```java
3. Approach 3: Recursion
class Solution {
    public void reverseString(char[] s) {
        solution(s,0,s.length-1);
    }

    private void solution(char[]s, int left, int right){
        if(left >= right) return;
        swap(s,left, right);
        solution(s, left+1, right-1);

    }

    private void swap(char[] s, int left, int right){
        char temp = s[left];
        s[left] = s[right];
        s[right] = temp;
    }
}

```

5.	Longest Substring Without Repeating Characters
```

```

```java


```

6.	Group Anagrams
```
https://leetcode.com/problems/group-anagrams/description/
https://takeuforward.org/practice/dsa/group-words-by-anagrams
```

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        HashMap<String,List<String>> hm = new HashMap<>();

        for(String str : strs){
            char charArr[] = str.toCharArray();
            Arrays.sort(charArr);

            String sorted = new String(charArr);
            if(!hm.containsKey(sorted)){
                hm.put(sorted, new ArrayList<String>());
            }
            hm.get(sorted).add(str);
        }

       // List<List<String>> ans = new ArrayList<>();
        // for(List<String> list : hm.values()){
        //     ans.add(list);
        // }

        return new ArrayList<>(hm.values()); 
    }
}
Complexity Analysis
Time Complexity: O(n × m log m), where n is the number of strings and m is the maximum length of a string (due to sorting each string).
Space Complexity: O(n × m), for storing the grouped strings in the map.
```
```java
class Solution {
 
    // Method to group anagrams
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> groups = new HashMap<>();  // Hash map to store groups of anagrams
        
        // Loop through each word in the input array
        for (String word : strs) {
            int[] freq = new int[26];  // Frequency array for storing letter counts (26 lowercase English letters)
            
            // Count the frequency of each character in the word
            for (char c : word.toCharArray()) {
                freq[c - 'a']++;
            }
            
            // Create a key based on the frequency array
            StringBuilder key = new StringBuilder();
            for (int count : freq) {
                key.append('#').append(count);  // Append frequency count with a separator
            }
            
            // Group words with the same frequency pattern
            groups.putIfAbsent(key.toString(), new ArrayList<>());
            groups.get(key.toString()).add(word);
        }
        
        // Return the grouped anagrams as a list of lists
        return new ArrayList<>(groups.values());
    }
}
Complexity Analysis
Time Complexity: O(n × m), where n is the number of strings and m is the maximum string length.
Space Complexity: O(n × m), for storing frequency maps and groups.
```
