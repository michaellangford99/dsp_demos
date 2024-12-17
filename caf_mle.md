
$$s_0(t) = s(t-\tau_0)e^{j2\pi f_0t}$$

$$x(t) = s_0(t) + w(t)$$

$$x(t) = s(t-\tau_0)e^{j2\pi f_0t} + w(t)$$

where $w(t) \sim \mathcal{N}(0, \sigma^2)$

Parameter vector:

$$ \bar\theta = \{\tau_0, f_0\}$$

Parameterizes distribution of recieved signal:

$$p(\bar X; \tau_0,f_0)$$

(distribution of recieved signal time function x(t), sampled and represented as a random vector $\bar X$, parameterized by parameter vector $\bar \theta$)


$\bar X$ is then a signal vector embedded in additive white noise, and is distributed as:
(So because this signal is complex, and w[n] is real, *I think* I can use the 'dagger' operator for conjugate transpose on the vector)
(I'm doing this partly because it makes sense, and partly because it's how I get to a sane answer. I still don't think it's right, because it aught to be argmax  of  abs(X(tau, f)), not argmax  Re(X(tau, f)). So I'm definitely doing something wrong here.)

$$p(\bar X; \bar \theta) = \frac{1}{(2\pi \sigma^2)^{N/2}}e^{-\frac{1}{2}(\bar X - \bar s_0)^\dagger(\bar X - \bar s_0)}$$

Explicitly sample $x(t)$:

$$t = n\Delta t, n_0 = \frac{\tau_0}{\Delta t}$$

$$x[n] = x(n\Delta t)$$

$$x[n] = s[n - n_0] e^{j2\pi f_0 n \Delta t} + w[n]$$

Then expanding $\bar X$ and $\bar s_0$

$$p(\bar X, \bar \theta_0) = \frac{1}{(2\pi \sigma^2)^{N/2}}exp\left(-\frac{1}{2}\sum_{n=-\infty}^{\infty}(x^*[n] - s^*[n-n_0]e^{-j2\pi f_0n\Delta t})(x[n] - s[n-n_0]e^{j2\pi f_0n\Delta t})\right)$$

$$p(\bar X, \bar \theta_0) = \frac{1}{(2\pi \sigma^2)^{N/2}}exp\left(-\frac{1}{2}\sum_{n=-\infty}^{\infty}
|x[n]|^2 - x[n]s^*[n-n_0]e^{-j2\pi f_0n\Delta t} - x^*[n]s[n-n_0]e^{j2\pi f_0n\Delta t}
+s[n-n_0]s^*[n-n_0]e^{0}
\right)$$

$$p(\bar X, \bar \theta_0) = \frac{1}{(2\pi \sigma^2)^{N/2}}exp\left(-\frac{1}{2}\sum_{n=-\infty}^{\infty}
|x[n]|^2 - x[n]s^*[n-n_0]e^{-j2\pi f_0n\Delta t} - x^*[n]s[n-n_0]e^{j2\pi f_0n\Delta t}
+|s[n-n_0]|^2
\right)$$

MLE of parameter vector:

$$\hat{\bar \theta} = MLE \{ \bar \theta \} = \underset{\bar \theta}{textnormal{argmax} } p(\bar X; \bar \theta)$$

$$\hat{\bar \theta} = \underset{\bar \theta}{textnormal{argmax} } \frac{1}{(2\pi \sigma^2)^{N/2}}exp\left(-\frac{1}{2}\sum_{n=-\infty}^{\infty}
|x[n]|^2 - x[n]s^*[n-n_0]e^{-j2\pi f_0n\Delta t} - x^*[n]s[n-n_0]e^{j2\pi f_0n\Delta t}
+|s[n-n_0]|^2
\right)$$

$$ = \underset{\bar \theta}{textnormal{argmin} } \sum_{n=-\infty}^{\infty}
|x[n]|^2 - x[n]s^*[n-n_0]e^{-j2\pi f_0n\Delta t} - x^*[n]s[n-n_0]e^{j2\pi f_0n\Delta t}
+|s[n-n_0]|^2
$$

$\sum|x[n]|^2$ is constant w.r.t the parameter vector, and so is $\sum|s[n-n_0]|^2$, due to the limits of the integral not being affected by the index shift. 

$$ = \underset{\bar \theta}{\textnormal{argmax}} \sum_{n=-\infty}^{\infty}
x[n]s^*[n-n_0]e^{-j2\pi f_0n\Delta t} + x^*[n]s[n-n_0]e^{j2\pi f_0n\Delta t}
$$

$$y[n] = x[n]s^*[n-n_0]e^{-j2\pi f_0n\Delta t}$$

$$ = \underset{\bar \theta}{textnormal{argmax} } \sum_{n=-\infty}^{\infty}
y[n] + y^*[n]
$$

$$ = \underset{\bar \theta}{textnormal{argmax} } \sum_{n=-\infty}^{\infty}
2 \mathbb{R}e[y[n]]
$$

$$ = \underset{\bar \theta}{textnormal{argmax} } \sum_{n=-\infty}^{\infty}
\mathbb{R}e[x[n]s^*[n-n_0]e^{-j2\pi f_0n\Delta t}]
$$

Summation and $\mathbb{R}e$ are interchangeable

$$ = \underset{\bar \theta}{textnormal{argmax} } \mathbb{R}e\left[\sum_{n=-\infty}^{\infty}
x[n]s^*[n-n_0]e^{-j2\pi f_0n\Delta t}\right]
$$

This is identical to the form of the discretized CAF (aside from a multiplicative constant $\Delta t$), leaving:


$$ = \underset{\bar \theta}{textnormal{argmax} } \mathbb{R}e\left[\chi[n, k]\right]$$

(introducing frequency discretization of $k\Delta f = f_0$ as well)

Again, I'm confident it aught to be $\underset{\bar \theta}{textnormal{argmax} } \left|\chi[n, k]\right|$, but this is what I got. I'm not sure where I went wrong, but this is where I'm at right now.