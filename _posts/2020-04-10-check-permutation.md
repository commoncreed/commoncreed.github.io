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

- Describe what it means for two strings to be permutations of each other. Now, look at
that definition you provided. Can you check the strings against that definition? 
- There is one solution that is 0 (N log N) time. Another solution uses some space, but
is O(N) time. 
- Could a hash table be useful?
- Two strings that are permutations should have the same characters, but in different
orders. Can you make the orders the same?

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