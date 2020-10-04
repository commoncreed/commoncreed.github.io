---
id: 101
title: "Check Permutation"
date: 2020-10-04T15:44:43+00:00
author: admin
layout: single
comments_id: 101
categories:
  - Data Structures and Algorithms
  - Cracking The Coding Interview
---

Implement an algorithm to determine if a string has all unique characters. What if you can not use additional data structures?

#### Hints

- Try a hash table.
- Could a bit vector be useful?
- Can you solve it in O(N log N) time? What might a solution like that look like?

#### Solution


Sort the strings.

{% highlight java %}
public static String sort(String s) {
  char[] content = s.toCharArray();
  java.util.Arrays.sort(content);
  return new String(content);
}

public static boolean permutation(String s, String t) {
  return sort(s).equals(sort(t));
}	
{% endhighlight %}

Check if the two strings have identical character counts.

{% highlight java %}
public static boolean permutation(String s, String t) {
  if (s.length() != t.length()) return false; // Permutations must be same length
  
  int[] letters = new int[128]; // Assumption: ASCII
  for (int i = 0; i < s.length(); i++) {
    letters[s.charAt(i)]++;
  }
    
  for (int i = 0; i < t.length(); i++) {
    letters[t.charAt(i)]--;
      if (letters[t.charAt(i)] < 0) {
        return false;
      }
  }
    
  return true; // letters array has no negative values, and therefore no positive values either
}
{% endhighlight %}

If we can't use additional data structures, we can do the following: 

1. Compare every character of the string to every other character of the string. This will take O( n2) time
and 0 (1) space.
2. If we are allowed to modify the input string, we could sort the string in O( n log( n» time and then
linearly check the string for neighboring characters that are identical. Careful, though: many sorting
algorithms take up extra space. 