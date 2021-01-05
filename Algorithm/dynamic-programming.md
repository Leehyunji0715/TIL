### Reference (What I study with)
[Dynamic Programming - Learn to Solve Algorithmic Problems & Coding Challenges](https://www.youtube.com/watch?v=oBt53YbR9Kk)<br/>
[LeetCode - 10.Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)<br/>

## Problem on general recursion (재귀함수의 문제점)
- Recursively constructed function could take long time to return result.<br/>For example, there's Fibonacci function (int fib(n)).<br/>When n is big enough like 50, it takes long long time.<br/>
	- It does ==duplicated== works.

## Memoization
When we draw tree of fib(7) graph, we can see several subtrees like fib(3), fib(4) and etc. The values are duplicated and it increases time complexity.<br/>
==We use value once calculated before==in recursion<br/>
Therefore, in "fib(n)" example, we add separate variable that can hold fib(n) results. Then, when the value is in the storage, we just return the existed value not recalculating it. 




### Light Note
When I tried to solve problem #10 in 'leetcode', it says the problem is related to DP(Dynamic Programming).<br/>
Thisi is what I studied to solve it.<br/>



