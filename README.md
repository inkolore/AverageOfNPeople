# Setup of the problem
There is a saying that we are the average of the $N$ closest people to us, where $N = 5$ or $N = 10$.
So what happens if also consider that each of those $N$ people is the average of you and the other $N-1$ people? How do we solve the system?
This is the setup of the problem, and the result for a rather general type of 'average functions' is that this is only possible if
$$ x_1 = x_2 = ... = x_N, $$
in other words every value must be equal.

# Weight f-mean function
The general type of average function I used is the $f$-mean function, where $f$ is an invertible and increasing function.
The average $y$ is defined as
$$ y = f^{-1} \left( \dfrac{1}{|\omega|} \sum_{j=1}^N \omega_j f(x_j) \right), $$
where $|\omega|$ is the sum of the weights.

This type of function satisfies the main property of an average, being that it is between the minimum and the maximum of the $x_i$ points.
