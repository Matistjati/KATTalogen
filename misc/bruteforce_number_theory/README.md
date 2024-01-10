# Brute force number theory
Sometimes, algorithms run much faster than one would expect due to some quantity being unexpectedly small. Here is a non-comprehensive list of some of these.

## Divisors
First off, some definitions. A number is a prime factor if it divides a given number and is a prime. A number is a divisor if divides a given number.

Let's start by bounding the number of prime factors of a number. Obviously, the smaller the prime factors are, the more we can have. The smallest prime is $2$, thus a number of size $n$ can have at most $\approx \log_2(n)$ prime factors. This is an upper bound, and is usually smaller for most $n$ in practice.

How might we then bound the number of divisors? A trivial bound is that we can either choose or not choose each prime factor, leading to $2^{\log_2(n)}=n$ divisors. This turns out to be a gross overestimate.

Let $d(n)$ denote the number of divisors of n. Suppose that $n=p_1^{k_1}\cdot p_2^{k_2} \cdots p_n^{k_n}$. Then, $d(n)=(k_1+1)\cdot(k_2+1)\cdots(k_n+1)$. What we are interested in is $d_{max}(n)=max(d(1),d(2),\dots,d(n))$, i.e., the "most evil" number less than $n$. 

It turns out that $d_{max}(n)=o(n^{\epsilon})$ for all $\epsilon > 0$, meaning that it essentially stops growing meaningfully for sufficiently large $n$. In practice, our numbers are not sufficiently large. Thus, a good rule of thumb is

$$d_{max}(n)=n^{\frac{1}{3}}$$

If you want to be more precise, here are some approximate values of $d_{max}(n)$:\
$d_{max}(10^6)\approx240$\
$d_{max}(10^9)\approx1300$\
$d_{max}(10^{12})\approx6700$\
$d_{max}(10^{15})\approx27000$\
$d_{max}(10^{18})\approx10^5$

A more exhaustive list can be found [here](https://gist.github.com/dario2994/fb4713f252ca86c1254d).

The biggest practical implication of this is that we can factor any number we will realistically encounter using [pollard-rho](https://github.com/kth-competitive-programming/kactl/blob/main/content/number-theory/Factor.h) in $O(n^{\frac{1}{4}})$ and then generate all its divisors in $O(d(n))$ using a simple recursive function. This allows you to trivialize some number theoretic problems.

Problems using the fact that there are few divisors:\
[Dual divisibility](https://open.kattis.com/problems/dualdivisibility)\
[Gcd and lcm](https://open.kattis.com/problems/gcdandlcm)\
[Evening out 2](https://open.kattis.com/problems/eveningout2)\
[Positive divisors](https://open.kattis.com/problems/positivedivisors)\
[Inheritance](https://open.kattis.com/problems/inheritance)\
[List game 2](https://open.kattis.com/problems/listgame2)\
[Gcd sum.](https://open.kattis.com/problems/gcdsum) (Hint: numbers such that $d_{max}(n)=d(n)$ are called highly composite numbers. These are super rare and are the worst case. The test data is weak, so you can get accepted by precomputing the answer for all highly composite numbers.)

## Sum of divisors

One can also show that $\sum_{i=1}^{n}d(n)\approx n \cdot \log(n)$. One possible use case is to compute a product-style convolution:

$$C[k]=\sum_{i*j=k}a[i]\cdot b[j]$$

In $O(|C|\cdot \log(|C|))$ time. In order to compute this, we will need to quickly factor all numbers less than $n$ .
A generally useful number-theoretic primitive is the "smallest-factor sieve". You basically execute the sieve of eratosthenes, but for each number you save its smallest prime factor. Using this, you can factor a number in $O(\log(n))$ by repeatedly dividing it by its smallest prime factor after sieving.

Problems:\
[Variable names](https://open.kattis.com/problems/variabelnamn) (only uses sum of divisors, not the convolution)

## Partitions

Let $p(n)$ denote the number of sorted sets with sum $n$. This function grows fairly, but usually not prohibitively quickly (problems based on solving problems in $O(p(n) \cdot poly(n))$ usually have their limits set accordingly). A good approximation is

$$p(n)\approx0.145/n\cdot e^{2.56\sqrt{n}}$$

Some notable values are:\
$p(9)=30$\
$p(20)=627$\
$p(50)\approx 2 \cdot 10^5$\
$p(100)\approx 2 \cdot 10^8$

If one needs to compute $p(n)$ exactly, it can be done rather trivially using dynamic programming.

Problems:\
[sum 41](https://www.facebook.com/codingcompetitions/hacker-cup/2023/round-1/problems/B2?source=google)\
[Explosion exploit](https://open.kattis.com/problems/explosion)\
[Youndiagram](https://po.kattis.com/problems/young)

## Products
Quite surprisingly, the number of sorted sets whose product is less than $n$ is asymptotically $n^{1+o(1)}$. Proving this is quite difficult.

Problems:\
[Sequence](https://boi23.kattis.com/problems/boi23.sequence)
