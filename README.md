# AverageOfNPeople
A meme problem I nerdsniped myself into solving

# Initial problem
The initial problem was about solving the system
$$
\begin{cases}
x_0 &= \dfrac{1}{N} \sum_{j=1}^N x_j \\[2mm]
x_1 &= \dfrac{1}{N} \left( x_0 + \sum_{j=2}^N x_j \right) \\
\cdots \\
x_N &= \dfrac{1}{N} \left( \sum_{j=0}^{N-1} x_j \right),
\end{cases}
$$
which is the old adage that we are the average of the $N$ closest people to us. We can check with the usual techniques to solve linear systems that the only solutions are of the form
$$
x_0 = x_1 = \cdots = x_N.
$$
This result is much more general however.

# The weighted f-mean
The result applies to a more general notion of average, the weighted $f$-mean, which we define here as
$$
\begin{align*}
y &= \text{mean}_{f, \omega}^N (x_1, \cdots, x_N) \\
&:= f^{-1} \left( \dfrac{1}{|\omega|} \sum_{j=1}^N \omega_i f(x_j) \right),   
\end{align*}
$$
where $f$ is any invertible function, and $|\omega| := \sum_{j=1}^N \omega_j$, with $\omega_j \geq 0$ and at least one $\omega_i > 0$. \\

Example of averages which can be expressed this way:
\begin{itemize}
\item The arithmetic mean for $f = id$ and uniform weights
\item The geometric mean for $f = log(.)$ and uniform weights
\item The harmonic mean for $f : x \mapsto 1/x$ and uniform weights
\item The $L_p$ mean for $f : x \mapsto x^p$ and uniform weights
\item The weighted arithmetic mean for $f = id$ and the corresponding weights
\end{itemize}
though this does not consider statistics such as the median or quantiles. \\

Here are the basic properties of the weighted $f$-mean: \\

1 - If $f$ is an increasing function, then the weighted $f$-mean is such that is between the minimum and the maximum of the $N$ points:
$$
\text{min}_{j \in \{1, \cdots, N\}} x_j
\leq \text{mean}_{f, \omega}^N (x_1, \cdots, x_N)
\leq \text{max}_{j \in \{1, \cdots, N\}} x_j.
$$
In particular, if the $N$ points are all equal to the same constant: $x_1 = x_2 = \cdots = x_N = c$, then the weighted $f$-mean is also equal to $c$. \\

This result is immediate from the definition. If we assume for instance that the minimum (respectively maximum) of the $x$ points is given by $x_1$ (resp. $x_N$), then for an increasing function $f$ we know that
\begin{align*}
f(x_1) = \dfrac{1}{|\omega|} \sum_{j=1}^N \omega_j f(x_1)
\leq &\dfrac{1}{|\omega|} \sum_{j=1}^N \omega_j f(x_j)
\leq \dfrac{1}{|\omega|} \sum_{j=1}^N \omega_j f(x_N) = f(x_N) \\
\Rightarrow x_1
\leq &f^{-1} \left( \dfrac{1}{|\omega|} \sum_{j=1}^N \omega_j f(x_j) \right)
\leq x_N,
\end{align*}
which proves the claim. \\

2 - The weighted $f$-mean can be expressed as the weighted $f$-mean of two (or more) weighted $f$-means, in other words, it can decomposed. For instance, for $N = 5$, we note $|\omega_{1,2}| := \omega_1 + \omega_2$, which allows us to say that
\begin{align*}
\text{mean}_{f,\omega}^5 (x_1, x_2, x_3, x_4, x_5) &= f^{-1} \left( \dfrac{\omega_1 f(x_1) + \omega_2 f(x_2)}{|\omega|} + \dfrac{\omega_3 f(x_3) + \omega_4 f(x_4) + \omega_5 f(x_5)}{|\omega|} \right) \\
&= f^{-1} \left( \dfrac{|\omega_{1,2}|}{|\omega|} \dfrac{f(x_1) + f(x_2)}{|\omega_{1,2}|} + \dfrac{|\omega_{3,4,5}|}{|\omega|} \dfrac{f(x_3) + f(x_4) + f(x_5)}{|\omega_{3,4,5}|} \right) \\
&= f^{-1} \left( \dfrac{|\omega_{1,2}|}{|\omega|} f(\text{mean}_{f,\omega}^2 (x_1, x_2)) + \dfrac{|\omega_{3,4,5}|}{|\omega|} f(\text{mean}_{f,\omega}^3 (x_3, x_4, x_5))  \right),
\end{align*}
which means that
$$
f(\text{mean}_{f,\omega}^5 (x_1, x_2, x_3, x_4, x_5)) - \dfrac{|\omega_{1,2}|}{|\omega|} f(\text{mean}_{f,\omega}^2 (x_1, x_2)) = \dfrac{|\omega_{3,4,5}|}{|\omega|} f(\text{mean}_{f,\omega}^3 (x_3, x_4, x_5)),
$$
and the last line in particular will be useful to the reasoning that follows.

Note that in order to apply this decomposition, the sum of weights $|\omega_{1,2}|$ and $|\omega_{3,4,5}|$ couldn't be zero. An easy fix to insure this can never happen is to assume that for all weights: $\omega_j > 0$.

# The more general case
In order to write the system more neatly, let's denote by a hat a missing element, such that
$$
(x_1, x_2, \cdots, x_N) = (\hat{x_0}, x_1, x_2, \cdots, x_N).
$$
Moreover, we will use a similar notation for the $\omega$ vectors, such that
$$
\omega_{\hat{0}} := (\hat{\omega_0}, \omega_1, \cdots, \omega_N) = (\omega_1, \cdots, \omega_N).
$$

We wish to find the solutions of the following system:
$$
\begin{cases}
x_0 &= \text{mean}_{f,\omega_{\hat{0}}}^N (\hat{x_0}, x_1, \cdots, x_N) \\
x_1 &= \text{mean}_{f,\omega_{\hat{1}}}^N (x_0, \hat{x_1}, \cdots, x_N) \\
\cdots \\
x_N &= \text{mean}_{f,\omega_{\hat{N}}}^N (x_0, x_1, \cdots, \hat{x_{N}}),
\end{cases}
$$
for an increasing and invertible function $f$ and a vector of weights $\omega$ such that $\omega_j > 0$ for all $j$. \\
Note that this form of the system implies that the weights depend only on the $x_i$ it is assigned to, and not on the line of the system. We won't treat here the more general case where we have a \textbf{matrix} of weights, where each line can contain weights independent of the other lines. \\

Because of the symmetry of the problem, we can assume that
$$
x_0 \leq x_1 \leq \cdots \leq x_N.
$$
Thus, $x_N \geq x_{N-1}$, and because of the last line of the system, we know that
$$
x_0 \leq x_N \leq x_{N-1},
$$
since the weighted $f$-mean is between the minimum and the maximum of the data points. As a result, $x_N = x_{N-1}$. \\

With the second to last line of the system, we know that
$$
f(x_{N-1}) = \dfrac{\omega_N f(x_N)}{|\omega_{\hat{N-1}}|} + \dfrac{\omega_0 f(x_0) + \cdots + \omega_{N-2} f(x_{N-2})}{|\omega_{\hat{N-1}}|},
$$
which allows us to use the decomposing property of the weighted $f$-mean. Since $x_N = x_{N-1}$ and $|\omega_{0,\cdots, N-2}| = |\omega_{\hat{N-1}}| - |\omega_{N}|$, we can thus rewrite:
\begin{align*}
\dfrac{|\omega_{\hat{N-1}}| f(x_{N-1}) - |\omega_{N}| f(x_N)}{|\omega_{0,\cdots, N-2}|} &= \dfrac{1}{|\omega_{0,\cdots, N-2}|} \sum_{j=0}^{N-2} \omega_j f(x_j) \\
\Rightarrow f(x_{N-1}) &= \dfrac{1}{|\omega_{0,\cdots, N-2}|} \sum_{j=0}^{N-2} \omega_j f(x_j) \\
\Rightarrow x_{N-1} &= \text{mean}_{f,\omega_{0, \cdots, N-2}}^{N-1} (x_0, \cdots, x_{N-2}).
\end{align*}
Since $x_{N-1} \geq x_{N-2}$ by our choice of ordering, we can thus once again say that $x_{N-1} = x_{N-2}$ since the $f$-mean is between the minimum and maximum of its data points. \\

The general case is treated in exactly the same way, though the notations become more tedious, such that we won't bother with writing the weights $\omega$ here, and are using the standard uniform weights. For $x_{N-k}$, we have that:
$$
f(x_{N-k}) = \dfrac{1}{N} \sum_{j=0}^{k-1} f(x_{N-j}) + \dfrac{1}{N} \sum_{j=k+1}^{N} f(x_{N-j}),
$$
and by induction $x_{N-k} = \cdots = x_{N}$. Thus, we can once again rewrite:
\begin{align*}
\dfrac{N f(x_{N-k}) - \sum_{j=0}^{k-1} f(x_{N-j})}{N-k} &= \dfrac{1}{N-k} \sum_{j=k+1}^{N} f(x_{N-j}) \\
\Rightarrow f(x_{N-k}) &= \dfrac{1}{N-k} \sum_{j=k+1}^{N} f(x_{N-j}) \\
x_{N-k} &= \text{mean}_f^{N-k} (x_0, \cdots, x_{N-k-1}),
\end{align*}
which once again implies that $x_{N-k} = x_{N-k-1}$. \\

Thus, by induction, we showed that
$$
x_N = x_{N-1} = \cdots = x_0.
$$

# To go further
The first generalization would be to consider a matrix weight, instead of simply a system where the weights $\omega_i$ only depend on the point $x_i$ it is assigned to. \\

A further generalization of the average, as explained on \url{https://en.wikipedia.org/wiki/Average#Miscellaneous_types}, is to define for a function $g$ which is continuous, strictly increasing and symmetric in its $n$ arguments, the average $y$, which is the value such that
$$
g(x_1, x_2, \cdots, x_N) = g(y, y, \cdots, y).
$$
This form generalizes the $f$-mean, since it allows for $g = \max$ and similar other functions, such as the median or the quantiles. \\

While this average satisfies the property of being between the minimum and maximum of the data points, it is unclear to me whether we can derive the same property of decomposition, or whether we can solve the system in another way.
