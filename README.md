# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.


The if statement is just constant time so 1. The else statment does n/3 recursively 3 times so 3T(n/3). Count is constant so add 1. The outter most for loop runs $n^2$ times, the first nested loop runs n times and the inner most for loop runs $n^2$ times. So you get $n^2 * n * n^2 = n^5$ after you disregrard the constant times from the if statement and the var count.

So, to start we have:<br> $T(n) = 1$, <br> $3T(n/3) + n^5$ , <br> $3(3T((n/3)/3) + ( (n/3)^5) + n^5$ = $9T(n/9) + 3(n/3)^5 +n^5$. <br> Then we get $log_3n$ from the three levels of recursion $\frac{n}{3^i} = 1$ <br> 
1 because the recursion happens until the size equals 1. <br>
$n=3^i$<br>
$i=log_3n$
So, sub in $i$ for the unfolding<br>
$3^iT(n/3^{i}) + \sum_{k=0}^{i-1} 3^{i}\* (n/3^i)^5$ and use summation for the count increasing for the nested loop that happens $n^5$ times.
$3^{log_3n}T(n/3^{log_3n}) + \sum_{k=0}^{log_3n-1} 3^{log_3n}\* (n/3^{log_3n})^5$<br>
this summation will equal $n^5$ after adding each iteration in the recursive call.<br>
So getting in $n*T(1)+n^5$ we know this runtime analysis is $\in(n^5)$<br>


Chapter 3, pages 49-51 from intro to algorithms book<br>
Mainly slides 1-20 but I looked over the whole thing<br>
https://www.khoury.northeastern.edu/home/lieber/courses/algorithms/cs5800/sp14/help-sessions/slides/recurrences.pdf

"I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice."
