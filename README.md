Download Link: https://assignmentchef.com/product/solved-stats506-problem-set-3
<br>
<h1>Question 1</h1>

First, repeat question 3 parts a-c from problem set 1 using data.table for all computations and data manipulations.

Then, formulate and state a question answerable using the RECS data. Your question should be similar in scope to (one of) parts a-c above and should rely on one or more variables not previously used. Answer your question (using data.table) and provide supporting evidence in the form of nicely formatted graphs and/or tables.

<h1>Question 2</h1>

In this question you will design a Monte Carlo study in R to compare the performance of different methods that adjust for <a href="https://xkcd.com/882/">multiple comparisons (https://xkcd.com/882/)</a>. You can read more about each of these methods by referring to help(p.adjust) in R and the references listed there.

Throughout this question, let <em>n</em>= 1000, <em>p </em>= 100 and

<em>β<sub>i </sub></em>= { 01        else<em>i </em>∈ .{1, … , 10},

Let <em>X </em>∈ℝ<em><sup>n</sup></em>×<em><sup>p</sup></em> with <em>X </em>∼ <em>N</em>(0<em><sub>p</sub></em>, Σ) and <em>Y </em>∼ <em>N</em>(<em>Xβ</em>, <em>σ</em><sup>2</sup><em>I<sub>p</sub></em>) where <em>I</em> is a <em>p </em>× <em>p</em> diagonal matrix.

<ol>

 <li>Write a function that accepts matrices X and beta and returns a p by mc_rep matrix of p-values corresponding to p-values for the hypothesis tests:</li>

</ol>

<em>H</em><sub>0 </sub>: <em>β<sub>i </sub></em>= 0, <em>H</em><sub>1 </sub>: <em>β<sub>i </sub></em>≠ 0.

In addition to X and beta your function should have arguments sigma ( <em>σ</em>) and mc_rep controlling the error variance of

<em>Y</em> and number of Monte Carlo replicates, respectively. Your function should solve the least-squares problems using the QR decomposition of

<em>X</em><sup>′</sup><em>X</em>. This decomposition should only be computed once each time your function is called. i. Refer to the course notes to find <em>β</em>̂.

<ol>

 <li>Use <em>Y</em> and <em>Y</em><sup>̂ </sup>= <em>Xβ</em>̂ to estimate the error variance for each Monte Carlo trial <em>m</em>:</li>

</ol>

<em>n</em>

<em>σ</em>2<em>m</em>̂ =    <em>n</em>−<u>1 </u><em>p </em>∑<em>i</em>= 1 (<em>Y</em><em>im </em>− <em>Y</em>̂<em>im</em>)2

<ul>

 <li>Use the result from ii and the QR decomposition to find the variance of <em>β</em><sup>̂</sup><em><sub>i</sub></em>, <em>v<sub>i </sub></em>= <em>σ</em><sup>2</sup>̂ (<em>X</em><sup>′</sup><em>X</em>)− 1.</li>

</ul>

[Note: you will need to do some algebra to determine how to compute (<em>X</em><sup>′</sup><em>X</em>)− 1 using Q and R.

Or you can use the function chol2inv() .] iv. Form <em>Z<sub>i </sub></em>= <em>β</em><sup>̂</sup><em><sub>i</sub></em>/<em>v<sub>i</sub></em> and find <em>p </em>= 2(1 − Φ<sup>− 1</sup>(|<em>Z<sub>i</sub></em>|)).

Test your function with a specific <em>X</em> and <em>Y</em> by comparing to the output from appropriate methods applied to the object returned by lm(Y ~ 0 + X) . It’s okay if there is some finite precision error less than ~1e-3 in magnitude. Hint: use set.seed() to generate the same <em>Y</em> inside and outside the scope of the function for the purpose of testing.

<ol>

 <li>Choose Σ and <em>σ</em> as you like. Use the Cholesky factorization of Σ to generate a single <em>X</em>. Pass <em>X</em>, <em>β</em>, and <em>σ</em> to your function from the previous part.</li>

 <li>Write a function evaluate that takes a set of indices where <em>β</em>≠ 0 and returns Monte Carlo estimates for the following quantities:</li>

</ol>

The family wise error rate

The false discovery rate

The sensitivity

The specificity

See this <a href="https://en.wikipedia.org/wiki/Sensitivity_and_specificity#Sensitivity_index">page (https://en.wikipedia.org/wiki/Sensitivity_and_specificity#Sensitivity_index)</a> for additional details.

<ol>

 <li>Apply your function from the previous part to the matrix of uncorrected P-values generated in part B.</li>

</ol>

Use the function p.adjust() to correct these p-values for multiple comparisons using ‘Bonferroni’, ‘Holm’, ‘BH’ (Benjamini-Hochberg), and ‘BY’. Use your evaluate() function for each set of adjusted p-values.

<ol>

 <li>Produce one or more nicely formatted graphs or tables reporting your results. Briefly discuss what you found.</li>

</ol>

<h1>Question 3</h1>

This is a bonus question related to problem 6 from the midterm. First, review the script written in Stata available <a href="https://github.com/jbhender/Stats506_F18/tree/master/solutions/PS3">here (https://github.com/jbhender/Stats506_F18/tree/master/solutions/PS3)</a>. In this question, you will work through various options for translating this analysis into R. You may submit all or some of these, but each part must be entirely correct to earn the points listed.

<ol>

 <li>Write a translation using table for the computations. [5 pts]</li>

 <li>Write a function to compute the univariate regression coefficient by group for an arbitrary dependent, independent, and grouping variables. Use table for computations within your function. Test your function by showing it produces the same results as in part a. [10 pts]</li>

 <li>Compute the regression coefficients using the dplyr verb summarize_at() . [5 pts]</li>

 <li>Write a function similar to the one in part b to compute arbitrary univariate regression coefficients by group. Use dplyr for computations within your function. You should read the “Programming with dplyr” vignette at vignette(‘programming’, ‘dplyr’) before attempting this. Warning: this may be difficult to debug! [10 points]</li>

</ol>