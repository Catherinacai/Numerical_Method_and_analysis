#2.2 **Fixed-Point Iteration**

##**An important thought about function equivalent**

suppose that we wish to solve the equation :
$$
f(x)=0 \tag{1}
$$
let $s$ to be one of the solution, them we have :
$$
f(s)=0  
$$
if we add s to both side of the equation we get : 
$$
f(s)+s=s
$$
let $g(x)=f(x)+x$ , then we can see that :
$$
g(x)=x \leftrightarrow f(x)=0
$$
**which tells us that solving the function $f(x)=0$ and the function $g(x)=x$ $(2)$ is equivalent.**

the reason why we change the equation  $(1)$ to  $(2)$ is that , we can conduct the iteration below :
with an initial guess $x_{0}$ we can generate a sequence :
$$
x_{n+1}=g(x_{n}) 
$$
by giving some regularization we can have the sequence converging to an element noted $x_{0}$ and $x_{0}$ is the solution of $(2)$


##**Error analysis**

Assume that $g$ is smooth enough for the analysis below.
let $s$ be a solution of $(2)$. We denote the error $x_{n}-s$ by $e_{n}$. Then the **Taylor series** of $g$ gives 
$$
\begin{align}
e_{n+1}&=x_{n+1}-s=g(x_{n})-g(s) \\
&=(x_{n}-s)g'(x)+\frac{(x_{n}-s)^2g''(x)}{2!}+\dots \\
&=e_{n}g'(s)+\frac{e_{n}^2g''(x)}{2!}+\dots \tag{3}
\end{align}
$$
the equation $(3)$ is important,  we will use that many time later.
If the sequence is to converge, we might reasonably require that the errors are being reduced with every iteration.
that is $|e_{n+1}|<|e_{n}|$ , 
it is necessary (neglecting the second- and higher-order terms) that $|g'(s)|<1$.


#2.3 **Newton's Method**

##**The main idea of the Newton's Method**

from the Error analysis above , we can see that the convergence of the sequence is of one order since $e_{n+1}=e_{n}g'(s)+o(e_{n})$ .  **By the equivalent principle above , the choices of $g$ can be various**.  If we establish different regularization to $g$ we will have different  ways to conduct our iteration . Thus the convergence speed of iteration sequences can be different.
**The Newton's Method is that we can let $g$ be chose to satisfy the condition $g'(s)=0$, under this condition the sequence {$x_{n}$} have second-order convergence**

Now we introduce another function $p(x)$ to the equation $(1)$
$$
f(x)=0 \leftrightarrow x=x+p(x)f(x) 
$$
provided that $p(x)$ has no zeros in the region of the solution.
$$
g(x)=x+p(x)f(x) \tag{4}
$$
then
$$
g'(x)=1+p'(x)f(x)+p(x)f'(x)
$$
since $f(s)=0$, 
$$
g'(s)=1+p(s)f'(s)=0
$$
which shows that by choosing :
$$
p(x)=\frac{1}{f'(x)}
$$
we have $g(x)=x+\frac{f(x)}{f'(x)}$, satisfying $g'(s)=0$

so the iteration formula itself is 
$$
x_{n+1}=x_{n}+\frac{f(x_{n})}{f'(x_{n})}
$$

##**Multiplicity circumstance**

The outcome above is under the assumption that $f(s)'\neq_{}0$

**What if $f'(s)=0$ of more generally $f^{(k)}(s)=0?$ **

Suppose then that we seek the solution s of $f(x) = 0$ and that $s$ is a double zero. That is
$$
f(s)=f'(s)=0, f''(s)\neq0$$
using L'Hôpital's rule, we have
$$
\begin{align}
g'(s)&=\lim_{ x \to s } \frac{f(x)f''(x)}{(f''(x))^2}=\lim_{ x \to s }\frac{(f(x)f'''(x)+f'(x)f''(x))}{2f'(x)f''(x)} \\
&=\frac{1}{2}+\lim_{ x \to s}\frac{f'(x)f''(x)}{2f'(x)f''(x)}\\ \\
&=\frac{1}{2}
\end{align}
$$

It follows that if we define a new iteration function $g_{2}$ by
$$
g_{2}(x)=x-\frac{2f(x)}{f'(x)}$$
then $g_{2}'(s)=0$
we can then conduct the literation using $g_{2}$ on the same way as $g$

**A similar argument can be applied to higher multiplicities of zeros. If $s$ is a zero with multiplicity $k$, then the modified Newton iteration
$$
x_{n+1}=g_{k}(x_{n})=x_{n}-\frac{kf(x_{n})}{f'(x_{n})} \tag{5}
$$
will exhibit quadratic convergence to $s$.**


##**Modified Newton algorithm**

the recovery of quadratic convergence is dependent on our knowing in advance of the computation that we seek a multiple zero. it cannot be assumed to be the normal situation. This raises the question of the practical value of this modified Newton algorithm

If $s$ is a zero with multiplicity $k$, then the general Newton iteration $x_{n+1}=x_{n}-\frac{f(x_{n})}{f'(x_{n})}$ is converging linearly to $s$. (since $g'(s)\neq 0$) 
It follows that as the limit is approached, the errors are related (for n sufficiently large) by $e_{n+1}\approx ce_{n}$ for some constant $c$
then 
$$
\begin{align}
\Delta x_{n}&=x_{n+1}-x_{n}=(x_{n+1}-s)-(x_{n}-s)\\ \\
&=e_{n+1}-e_{n}\approx e_{n}(c-1)
\end{align}
$$
from which we deduce in turn that
$$
\frac{\Delta x_{n+1}}{\Delta x_{n}}\approx \frac{e_{n+1}}{e_{n}}\approx c
$$
**It follows that the ratio of successive differences will be approximately constant
and that this constant is the linear convergence rate**

in fact, we can proof that for the general Newton iteration $c=g'(s)=\frac{k-1}{k}$,where $k$ is the multiplicity of root.
If the observed ratio of these differences is indeed a constant, $\overline c$ say, then we can recover $k$ in $(5)$  as the **nearest integer to $/(1 - \overline c)$**

Denote:
the consequence we have above is under the assumption of  n sufficiently large, so we have $c=g'(s)=\frac{k-1}{k}$. **If we want to use this approach to boost the convergence we should at first have the $x_{n}$ close to $s$, but once we have the $x_{n}$ close to $s$, there is no need to use this approach to boost the convergence.** Therefore, this method is very limited in practice.

**if the function $f$ have some roots that fairly close to each other, the approach may identify them as some multiple roots that lead to a definitely mistake**. for example , the function $f=(x-1.00001)(x-1.000013)(x-1.000015)$ may be treat as $f=(x-1.00001)^3$ in the approach which lead to choosing the function $g=x+\frac{3f}{f'}$,the literation will not converge to any root of $f$!


#2.4**The Secant Method**

##**central idea in computation**

the method above need us to count the $f'$ in computing. But for some functions $f$, we can't count their derivative analytically. we need to have efficient techniques at our disposal.

we have 
$$
f'(x_{n})\approx{\frac{f(x_{n})-f(x_{n-1})}{x_{n}-x_{n-1}}}
$$

so we may replace the Newton iteration formula with
$$
x_{n+1}=x_{n}-\frac{f(x_{n})-f(x_{n-1})}{x_{n}-x_{n-1}}f(x_{n})
$$

we can proof the rate of the convergence satisfy 
$$
e_{n+1}\approx ce_{n}^\alpha
$$
where $\alpha=\frac{{1+\sqrt{ 5 }}}{2}$
