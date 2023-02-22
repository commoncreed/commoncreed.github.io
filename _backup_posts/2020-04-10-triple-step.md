---
id: 101
title: "Triple Step"
date: 2020-10-04T15:44:43+00:00
author: admin
layout: single
comments_id: 101
categories:
  - Data Structures and Algorithms
  - Cracking The Coding Interview
tags:
  - Recursion and Dynamic Programming
---

A child is running up a staircase with n steps and can hop either 1 step, 2 steps, or 3 steps at a time. Implement a method to count how many possible ways the child can run up the
stairs. 

#### Hints

- Approach this from the top down. What is the very last hop the child made?
- If we knew the number of paths to each of the steps before step 100, could we compute the number of steps to 100?
- We can compute the number of steps to 100 by the number of steps to 99, 98, and 97. This corresponds to the child hopping 1, 2, or 3 steps at the end. Do we add those or multiply them?That is: Is it f(Hl0) = f(99) + f(98) + f(97) or f(100) = f(99) * f(98) * f(97)?
- We multiply the values when it's "we do this then this:' We add them when it's "we do this or this:"
- What is the runtime of this method? Think carefully. Can you optimize it?
- Try memoization as a way to optimize an inefficient recursive program.

#### Solution

##### Recursive: O(3<sup>n</sup>)

{% highlight java %}
public static int countWays(int n) {
  if (n < 0) {
    return 0;
  } else if (n == 0) {
    return 1;
  } else {
    return countWays(n - 1) + countWays(n - 2) + countWays(n - 3);
  }
}
{% endhighlight %}

##### Memoization: O(3n) ~ O(n)

{% highlight java %}
public static int countWays(int n) {
int[] map = new int[n + 1];
  Arrays.fill(map, -1);
  return countWays(n, map);
}

public static int countWays(int n, int[] memo) {
  if (n < 0) {
    return 0;
  } else if (n == 0) {
    return 1;
  } else if (memo[n] > -1) {
    return memo[n];
  } else {
    memo[n] = countWays(n - 1, memo) + countWays(n - 2, memo) + countWays(n - 3, memo);
    return memo[n];
  }
}
{% endhighlight %}

Regardless of whether or not you use memoization, note that the number of ways will quickly overflow the bounds of an integer. By the time you get to just n = 37, the result has already overflowed. Using a long will delay, but not completely solve, this issue. It is great to communicate this issue to your interviewer. He probably won't ask you to work around it

(although you could, with a BigInteger class), but it's nice to demonstrate that you think about these
issues. 