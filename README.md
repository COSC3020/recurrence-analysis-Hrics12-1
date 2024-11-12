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


When you unfold the algorithm it divides into 3 problems each size $(n/3)$<br><br>
The first level of recusion is: $T(n)=3T(n/3) + n^5$<br>
The second level (subbing in $T(n/3)$ = $T(n/3) = 3T(n/9) + (n/3)^5$<br>
Now put level two back into level one: $T(n)=3(3T(n/9)+(n/3)^5) + n^5$<br><br>
This simplifies to $T(n)= 9T(n/9) + 3 * \frac{n^5}{243} + n^5$<br>
The third level (subbing $T(n/9)$ = $T(n/9) = 3T(n/27) + (n/9)^5$<br>
Then put it back into the second level: $T(n) = 9(3T(n/27) + (n/9)^5) + 3 * \frac{n^5}{245} + n^5$<br>
this simplifies to $T(n) = 27T(n/27) + 9 * \frac{n^5}{59049} + 3 * \frac {n^5}{243} +n^5$

The pattern at each $i^{th}$ can be represented in summation form: $3^iT(n/3^{i}) + \sum_{k=0}^{i-1} 3^{k}\* (n/3^k)^5$

We get $i=log_3(n)$
because the recursion stops at $n/3^i = 1$ <br>
$(n/3^i = 1) = (3^i = n) = (i=log_3(n))$

//chatGPT

$\sum_{k=0}^{i-1}3^k * (\frac{n}{3^k})^5 = \sum_{k=0}^{i-1}3^k * \frac{n^5}{3^{5k}} = \sum_{k=0}^{i-1}\frac{n^5}{3^{4k}}$<br>

Geometric series with a ratio of $(1/3^4) = (1/81)$ = $S=n^5\sum_{k=0}^{i-1} \frac{1}{3^{4k}}$

the sum of the geometric series is: $\frac{1-r^i}{1-r}$ where $r=\frac{1}{81}$<br>
since $\frac{1}{81^i} gets smaller for larger i the total work is dominated by $n^5$<br><br>
So, the work at all levels is dominated by the work done at the deepest recursion level where $n=1$<br>
the overal time complexity is $O(n^5)$




Chapter 3, pages 49-51 from intro to algorithms book<br>
Mainly slides 1-20 but I looked over the whole thing<br>
https://www.khoury.northeastern.edu/home/lieber/courses/algorithms/cs5800/sp14/help-sessions/slides/recurrences.pdf
I had to ask chatGPT for help with the summation after the unfolding

"I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice."
