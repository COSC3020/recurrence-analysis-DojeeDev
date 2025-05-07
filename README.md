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

### Analysis
```math
m(n) = \begin{cases}
1 & \text{if } n \le 1 \\
 3m(n/3) + n^5 & \text{if } n \ge 1
\end{cases}
```
Note: I was just trying to fit the pattern of before and didn't notice that when subbing in it's (n/3)^2 not (n^5)/3 leading to bad math. Andrew Thomas 

$m(n) = 2m(n/3) + n^5

Solve for m(n/3): $m(n/3) = 3m(n/3^2)+(n/3)^5$

Plug in: $ = 3(3m(n/3^2)+(n/3)^5)+ n^5 = 3^2 m(n/3^2) + n^5 + \frac{n^5}{3^4}$

Solve for $m(n/n^2) = 3m(n/3^3) + \frac{n^5}{3^{10}}$

Plug in: $ = 3^2 ( 3m(n/3^3) + \frac{n^5}{3^{10}} ) + n^5 + \frac{n^5}{3^4} = 3^3 m(n/3^3) + n^5 + \frac{n^5}{3^4}+ \frac{n^5}{3^8}$

i = lg n

general form: $3^i m(n/3^i) + \sum_{k=0}^{k=i}{n^5 3^{-4k}}$

Solving sum: $ S_i = \frac{a(1-r^n)}{1-r}, a = n^5, r = 3^{-4} , S_i = \frac{n^5(1-3^{-4i})}{1-3^{-4}}$

Plug into general form: $3^i m(n/3^i) + \frac{n^5(1-3^{-4i})}{1-3^{-4}}$

Plug in i: = $n \cdot m(1) + n^5(\frac{(1-n^{-4})}{1-3^{-4}} \in O(n^5)$




I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice.
