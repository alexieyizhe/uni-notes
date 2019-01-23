__                                                                                                                                                                                                                                                                           CS 240 | __ January 15, 2019

#Order Notation (cont)

### Relationship Between Order Notations

![image-20190115084400147](assets/image-20190115084400147.png)

###Additional Properties

__Identity rule:__ $f(n) \in \Theta(f(n))$

__Maximum rules:__ Suppose that $f(n) \gt 0$ and $g(n) \gt 0$ for all $n \geq n_0$. Then:

- $O(f(n) + g(n)) = O(max\{f(n), g(n)\})$
- $\Omega(f(n) + g(n)) = \Omega(max\{f(n), g(n)\})$

__Transitivity:__

- 



### Techniques

Suppose that $f(n) \gt 0$ and $g(n) \gt 0$ for all $n \geq n_o$. Suppose that $L = \lim\limits_{n \rightarrow \infty} \frac{f(n)}{g(n)}$ (in particular, that the limit exists). Then $f(n)\in$

1. $o(g(n))$ if $L = 0$
2. $\Theta(g(n))$ if $0 \lt L \lt \infty$
3. $\omega(g(n))$ if $L = \infty$

> **Ex. Let $f(n)$ be a polynomial of degree $d \geq 0$ ($f(n) = c_dn^d + c_{d-1}n^{d-1}+...+c_1n+c_o$) for some $c_d \gt 0$. Prove that $f(n) \in \Theta(n^d)$.**
>
> $\lim\limits_{n \rightarrow \infty} \frac{f(n)}{g(n)} = \lim\limits_{n \rightarrow \infty}[\frac{c_dn^d}{n^d}+\frac{c_{d-1}n^{d-1}}{n^d}+...+\frac{c_o}{n^d}] = c^d$
>
> Since the limit is a constant, by L'Hopital's rule, $f(n) \in \Theta(n^d)$.

> **Prove that $f(n) = n(2 + sin \ n\pi/2) \in \Theta(n)​$. Note that the limit of the $f(n)​$ does not exist.**
>
> Since the limit does not exist ($sin$ does not converge), we can't use L'Hopital's Rule. However, $f(n)$ is bounded:
>
> $n \leq n(2 + sin \ n\pi/2) \leq 3n  \ \ \ \forall n \geq 1$
>
> This bound will show us that $f(n) \in \Theta(n)$.



### Growth Rates

Typically, $f(n)$ can be very complicated and  $g(n)$ is chosen to be simple. Nevertheless, they are related.

1. If $f(n) \in \Theta(g(n))$, then the **growth rate**s of $f(n)$ and $g(n)$ are _the same._This means that we don't really care about the small things like elementary operations, or constants (usually).
2. If $f(n) \in o(g(n))$, then we say that the growth rate of $f(n)$ is _less than_ the growth rate of $g(n)$.
3. If $f(n) \in \omega(g(n))$, then we say that the growth rate of $f(n)$ is _greater than_ the growth rate of $g(n)$.

> **Ex. Compare the growth rates of $log \ n$ and $n$.**
>
> If we continue taking derivatives...
>
> $\lim\limits_{n \rightarrow \infty} \frac{log \ n}{n^d} = \lim\limits_{n \rightarrow \infty} \frac{\frac{1}{n}}{dn^{d-1}} = \lim\limits_{n \rightarrow \infty} \frac{1}{n^d} = 0$. 
>
> By the techniques shown above, $log \ n$ is $o(d)$ for $d \gt 0$.

> **Ex. Compare the growth rates of $(log \ n)^c$ and $n^d$ (where $c \gt 0$ and $d \gt 0$).**
>
> We have to use the chain rule for the first function. Rest is left as exercise.