

# Logarithms

The logarithm is a function with multiple useful properties. It is defined as the function such that $k^{log_k(x)}=x$. For most applications, we do not care what k is. The most common choices for $k$ are $10$ or $e$. In most programming languages, the function $log$ refers to $log_e$.

# Number of digits

Problem 1: [Inverse factorial](https://open.kattis.com/problems/inversefactorial).\
If we use C++, our numbers will be too large to be stored in any basic type and overflow. If we use python, we will get a TLE verdict. In order to solve the problem, we will use following fact: if we write a number in base 10, it will have $\lfloor log_{10}(x) \rfloor$ digits. Therefore, when $n>10$, the value of $\lfloor log_{10}(x!) \rfloor$ will be unique. It is easy to compute $log_{10}(n!)$, since this is simply the length of our input (meaning, we do not have to convert it to an int, an operation which causes TLE). We can thus compute $\lfloor log_{10}(1!) \rfloor$, $\lfloor log_{10}(2!) \rfloor$, $\lfloor log_{3}(n!) \rfloor$, $\dots$ and stop when it is equal to len(input).

It might seem like we will run into the same problem of overflow as before. It turns out that $log(x)$ has two properties that make this a reasonable computation:
1. $log(x)$ grows very slowly. For example, $log_{10}(10^{10})=10$, and $log_{10}(10^6!) \approx 10^7$
2. $log(a \cdot b)=log(a)+log(b)$. This allows us to compute $log(n!)$ in $O(1)$ if we know the value of $log((n-1)!)$, as $log(n!)=log((n-1)!)+log(n))$

Additional problems: \
[Beautiful primes](https://open.kattis.com/problems/beautifulprimes)


# Large intermediary values

Problem 2: [Stirlings approximation](https://open.kattis.com/problems/stirlingsapproximation).

As the approximation is very good, $\frac{n!}{S(n)}$ will be pretty small. However, $n!$ and $S(n)$ are too large to fit in a float. We can instead compute $e^{log(\frac{n!}{S(n)})}$. In order to do this, we will use multiple useful identities:
1. $log(a \cdot b)=log(a)+log(b)$
2. $log(\frac{a}{b})=log(a)-log(b)$
3. $log(a^b)=log(a) \cdot log(b)$

We can thus do the following manipulations:
$$log(\frac{n!}{S(n)})=log(n!)-log(S(n))$$
$log(n!)=log(n)+log(n-1)+\dots+log(1)$
$log(S(n))=log(\sqrt{2\pi n})+log(n^n)-log(e^n)=$
$log(\sqrt{2\pi n})+nlog(n)-nlog(e)$

Why does this work? One way to think of logarithms is that we transform our numbers into a form that can express the magnitude and the first numbers of exponentially large numbers. The precision loss primarily occurs in less significant digits, instead of our representation of the exponent. 

Additional problems: \
[Associative exponents](https://open.kattis.com/problems/associativeexponents) \
[Fleecing the raffle](https://open.kattis.com/problems/raffle)

# A note on precision

Often times, using your language's equivalent of double will suffice. If not, try long double. If not even that is enough, you can read up about Kahan's algorithm.  [Sample implementation](https://github.com/Matistjati/CP-templates/blob/master/content/number-theory/kahan.cpp).

# Minimize/maximize product

Problem 3: [Villager trading](https://open.kattis.com/problems/villagertrading) \
Consider the directed graph where each item is a node and the possible trades are the edges. Each edge will have a weight, being the ratio between the two items in the trade. If we can find a cycle in this graph, whose product of edge lengths is $>1$, and there is a path from the cycle to a trade giving us emeralds, the answer is yes. Otherwise, no.

Using the Bellman Ford algorithm to find the cycle of greatest product would work. However, as before, our intermediary values might become exponentially small or large. To solve this, we will instead change each edge weight.

Let $e_1,e_2, \dots e_n$ be the weights of some cycle. We will make the following transformation:
$e_1 \cdot e_2 \dots \cdot e_n \geq 1 \iff$ \
$log(e_1 \cdot e_2 \dots \cdot e_n) \geq log(1) \iff$ \
$log(e_1) + log(e_2) \dots + log(e_n)) \geq 0 \iff$ \
$-log(e_1) - log(e_2) \dots - log(e_n)) \leq 0$ 

In other words, by replacing each edge weight $e$ with $-log(e)$, our problem is the standard problem of finding a negative cycle. We also need to be able to quickly check whether there exists a path from a node in a negative cycle to the emerald. To do this, we reverse all edges and precompute all the nodes reachable from the emerald (these are the nodes that can reach the emerald).

Additional problems: \
[Closing the borders](https://open.kattis.com/problems/closingtheborders) \
[Exponentially fun problem](https://open.kattis.com/problems/exponentiallyfun) \
[Bond](https://open.kattis.com/problems/bond)  (Hint: [hungarian algorithm](https://github.com/kth-competitive-programming/kactl/blob/main/content/graph/WeightedMatching.h))

# Large averages
In problems asking us for a probability, it is not uncommon that our answer will be in the form $\frac{a+b+c+\cdots}{k}$. If both the numerator and denominator are exponentially large, it might be difficult to compute this, even if the value of the fraction has a reasonable value. 

We will instead compute 
$\frac{a+b+c+\cdots}{k}=\frac{a}{k}+\frac{b}{k}+\frac{c}{k}+\dots=e^{log(a-k)}+e^{log(b-k)}+e^{log(c-k)}+\cdots$

If the terms in the numerator and the denominator have some nice form, such as being binomial coefficients or powers, this approach might work.

Problems: \
[Kolkrabbaleikarnir](https://open.kattis.com/problems/kolkrabbaleikarnir) \
Last carrot (to be added)

# Logarithm-like function
In some problems, you need to work with exponentially large integers, but using logarithms will be too imprecise. Then you might want to consider the following function: $f(n)=$ the powers in the prime factorization of $n$. For example, $f(36)=2^2*3^2$ \
f satisfies all the following identities:
1. $f(a*b)=f(a)+f(b)$
2. $f(\frac{a}{b})=f(a)-f(b)$
3. $f(a^b)=b\cdot f(a)$ (where $b$ is an integer) 

Addition of $f(a)=2^2*3^2$ and $f(b)=2^3*5^1$ is defined as adding powers: $f(a)+f(b)=2^5*3^2*5^1$.

Problems: \
[Divisors](https://open.kattis.com/problems/divisors)
