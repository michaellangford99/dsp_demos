**Signal model and PDF**

First, the signal model. vector parameter embedded in gaussian noise, however each individual independant measurement has a unique covariance matrix.

$$ \bf{x}[n] = \bf{\theta}[n] + \bf{w}[n], \hspace{35pt} \bf{w}[n] \sim \mathcal{N}(0, \bf{C}[n])$$

PDF of single measurement, simple multivariate normal.

$$p(\bf{x}[n];\bf{\theta}) = \frac{1}{(2\pi)^{k/2}det(\bf{C}[n])^{1/2}}exp\left\{    -\frac{1}{2}(\bf{x}[n] - \bf{\theta})^T\bf{C}[n]^{-1}(\bf{x}[n] - \bf{\theta})      \right\}$$

$$\bf{X} = \{ x[n] | n \in 0..(N-1)\} $$

Since each measurement is independant, the total probability is the product of N measurements.

$$p(\bf{X};\bf{\theta}) = \prod_{n=0}^{N-1}\frac{1}{(2\pi)^{k/2}det(\bf{C}[n])^{1/2}}exp\left\{    -\frac{1}{2}(\bf{x}[n] - \bf{\theta})^T\bf{C}[n]^{-1}(\bf{x}[n] - \bf{\theta})      \right\}$$

$$p(\bf{X};\bf{\theta}) = \left[\prod_{n=0}^{N-1}\frac{1}{(2\pi)^{k/2}det(\bf{C}[n])^{1/2}} \right] exp\left\{    -\frac{1}{2} \sum_{n=0}^{N-1}\left[(\bf{x}[n] - \bf{\theta})^T\bf{C}[n]^{-1}(\bf{x}[n] - \bf{\theta}) \right]     \right\}$$

**MLE**

The maximum likelihood estimate $\hat{\bf{\theta}}_{mle}$ is the arg-max of the pdf parameterized by $\theta$.

$$\hat{\bf{\theta}}_{mle} = \arg\max_{\bf{\theta}} \left\{ p(\bf{X};\bf{\theta}) \right\}$$

$$\hat{\bf{\theta}}_{mle} = \arg\max_{\bf{\theta}} \left\{ \left[\prod_{n=0}^{N-1}\frac{1}{(2\pi)^{k/2}det(\bf{C}[n])^{1/2}} \right] exp\left\{    -\frac{1}{2} \sum_{n=0}^{N-1}\left[(\bf{x}[n] - \bf{\theta})^T\bf{C}[n]^{-1}(\bf{x}[n] - \bf{\theta}) \right]     \right\} \right\}$$

$$\hat{\bf{\theta}}_{mle} = \arg\max_{\bf{\theta}} \left\{ exp\left\{    -\frac{1}{2} \sum_{n=0}^{N-1}\left[(\bf{x}[n] - \bf{\theta})^T\bf{C}[n]^{-1}(\bf{x}[n] - \bf{\theta}) \right]     \right\} \right\}$$

$$\hat{\bf{\theta}}_{mle} = \arg\min_{\bf{\theta}} \left\{ \sum_{n=0}^{N-1}\left[(\bf{x}[n] - \bf{\theta})^T\bf{C}[n]^{-1}(\bf{x}[n] - \bf{\theta}) \right]     \right\} $$

To find the MLE from this quadratic expression, take the gradient with respect to $\theta$ and set to zero.

$$\bf{\nabla_{\theta}} \left[ \sum_{n=0}^{N-1}\left[(\bf{x}[n] - \bf{\theta})^T\bf{C}[n]^{-1}(\bf{x}[n] - \bf{\theta}) \right] \right] = 0$$



$$\bf{\nabla_{\theta}} \left[ \sum_{n=0}^{N-1}\left[(\bf{x}[n] - \bf{\theta})^T\bf{C}[n]^{-1}(\bf{x}[n] - \bf{\theta}) \right] \right] = \sum_{n=0}^{N-1}\bf{C}[n]^{-1}(\bf{x}[n] - \bf{\theta}) = 0 $$

Factor out and rearrange:

$$ 0 = \sum_{n=0}^{N-1}\bf{C}[n]^{-1}(\bf{x}[n] - \bf{\theta}) = \sum_{n=0}^{N-1}\left[     \bf{C}[n]^{-1}\bf{x}[n] - \bf{C}[n]^{-1}\bf{\theta}\right] = \sum_{n=0}^{N-1}\left[\bf{C}[n]^{-1}\bf{x}[n]\right] - \sum_{n=0}^{N-1}\left[\bf{C}[n]^{-1}\bf{\theta}\right]$$

Separate measurement data and parameter:

$$ \sum_{n=0}^{N-1}\left[\bf{C}[n]^{-1}\bf{x}[n]\right] = \sum_{n=0}^{N-1}\left[\bf{C}[n]^{-1}\bf{\theta})\right] = \left[\sum_{n=0}^{N-1}\bf{C}[n]^{-1}\right]\bf{\theta}$$

Label this matrix $A$ for simplicity

$$ \bf{A} = \left[\sum_{n=0}^{N-1}\bf{C}[n]^{-1}\right]$$

$$ \sum_{n=0}^{N-1}\left[\bf{C}[n]^{-1}\bf{x}[n]\right] = \bf{A\theta}$$

Multiply by inverse of $A$ to isolate $\theta$

$$ \bf{A}^{-1}\sum_{n=0}^{N-1}\left[\bf{C}[n]^{-1}\bf{x}[n]\right] = \bf{A}^{-1}\bf{A}\bf{\theta} = \bf{\theta}$$

Final form of MLE:

$$ \hat{\bf{\theta}}_{mle}  =  \left[\sum_{n=0}^{N-1}\bf{C}[n]^{-1}\right]^{-1}  \left[\sum_{n=0}^{N-1}\bf{C}[n]^{-1}\bf{x}[n]\right] $$

