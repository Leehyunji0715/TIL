### Reference (What I study with)
[Dynamic Programming - Learn to Solve Algorithmic Problems & Coding Challenges](https://www.youtube.com/watch?v=oBt53YbR9Kk)<br/>

## Problem on general recursion (재귀함수의 문제점)
- 재귀 안에서 똑같은 연산을 중복해서 하기 때문에 시간 복잡도가 높아진다. <br/>
예를 들어, 일반 재귀로 만든 피보나치 함수 fib(7)에서 fib(3), fib(4) 등 같은 값이 여러번 호출되고, 이때마다 같은 연산을 실시한다. 
- Recursively constructed function could take long time to return result.<br/>
For example, there's Fibonacci function (int fib(n)).<br/>
When n is big enough like 50, it takes long long time.<br/>
	- It does **duplicated** works.

## Memoization
- fib(7)를 그래프화 해보면, fib(3)이나 fib(4)를 나타내는 서브트리들을 확인할 수 있다.<br/> **Memoization에서 중요한 것은 처음 계산한 fib(3)이나 fib(4) 값들을 따로 저장해 두고 만약 해당하는 값이 있다면 가져다 쓴다는 것**이다.
- When we draw tree of fib(7) graph, we can see several subtrees like fib(3), fib(4) and etc. <br/>
The values are duplicated and it increases time complexity.<br/>
**We use value once calculated before** in recursion.<br/>
Therefore, in "fib(n)" example, we add separate variable(storage) that can hold fib(n) results. <br/>
Then, when the value is in the storage, we just return the existed value not recalculating it. 
<br/>

## Memoization recipe
유튜브 영상에서 나온 DP 설계 팁인데 간결하고 좋아서 남겼다. (DP tip in youtube video)
	
	Make it work (먼저 정확한 결과가 나오게 만든다!)
		- Visualize the problem as a tree
		- Implement the treee using recursion
		- Test it 
	Make it efficient (정확한 결과를 만든 후에 효율적으로 만든다!)
		- Add a memo object
		(memo object: storage that holds recursion value)
		- Add a base case to return memo values
		- Store return values into the memo


<br/><br/><br/><br/>
##### Light Note
When I tried to solve [#10.Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)<br/> in 'leetcode', it says the problem is related to DP(Dynamic Programming).<br/>



