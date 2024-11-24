---
layout: default
title: MLE of vector parameter in varied noise covariance
description: Drone Presentation

eleventyNavigation:
  key: slide_0
  parent: dsp_cv
  
date: 2000-00-01
  
---
<div class="carousel-item" style="height: 100%">
<h1 class="text-center mt-3">{{ title }}</h1>

<div class="container align-content-center" style="height: 100%">
<div class="row">
<div class="col-lg align-content-center">

$${x}[n] = \theta[n] + {w}[n], \hspace{35pt} {w}[n] \sim \mathcal{N}(0, {C}[n])$$

$$p({x}[n];\theta) = \frac{1}{(2\pi)^{k/2}det({C}[n])^{1/2}}exp\left\{    -\frac{1}{2}({x}[n] - \theta)^T{C}[n]^{-1}({x}[n] - \theta)      \right\}$$

$${X} = \{ x[n] | n \in 0..(N-1)\} $$

$$p({X};\theta) = \prod_{n=0}^{N-1}\frac{1}{(2\pi)^{k/2}det({C}[n])^{1/2}}exp\left\{    -\frac{1}{2}({x}[n] - \theta)^T{C}[n]^{-1}({x}[n] - \theta)      \right\}$$

$$p({X};\theta) = \left[\prod_{n=0}^{N-1}\frac{1}{(2\pi)^{k/2}det({C}[n])^{1/2}} \right] exp\left\{    -\frac{1}{2} \sum_{n=0}^{N-1}\left[({x}[n] - \theta)^T{C}[n]^{-1}({x}[n] - \theta) \right] \right\}$$

$$\hat{\theta}_{mle} = \argmax_{\theta} \left\{ p({X};\theta) \right\}$$

</div>
<div class="col-lg align-content-center">

$${\nabla_\theta} \left[ \sum_{n=0}^{N-1}\left[({x}[n] - \theta)^T{C}[n]^{-1}({x}[n] - \theta) \right] \right] = 0$$

$${\nabla_\theta} \left[ \sum_{n=0}^{N-1}\left[({x}[n] - \theta)^T{C}[n]^{-1}({x}[n] - \theta) \right] \right] = \sum_{n=0}^{N-1}{C}[n]^{-1}({x}[n] - \theta) = 0 $$

$$ 0 = \sum_{n=0}^{N-1}{C}[n]^{-1}({x}[n] - \theta) = \sum_{n=0}^{N-1}\left[     {C}[n]^{-1}{x}[n] - {C}[n]^{-1}\theta\right] = \sum_{n=0}^{N-1}\left[{C}[n]^{-1}{x}[n]\right] - \sum_{n=0}^{N-1}\left[{C}[n]^{-1}\theta\right]$$

$$ \sum_{n=0}^{N-1}\left[{C}[n]^{-1}{x}[n]\right] = \sum_{n=0}^{N-1}\left[{C}[n]^{-1}\theta)\right] = \left[\sum_{n=0}^{N-1}{C}[n]^{-1}\right]\theta$$

$$ {A} = \left[\sum_{n=0}^{N-1}{C}[n]^{-1}\right]$$

$$ \sum_{n=0}^{N-1}\left[{C}[n]^{-1}{x}[n]\right] = {A\theta}$$

$$ {A}^{-1}\sum_{n=0}^{N-1}\left[{C}[n]^{-1}{x}[n]\right] = {A}^{-1}{A}\theta = \theta$$

$$ \hat{\theta}_{mle}  =  \left[\sum_{n=0}^{N-1}{C}[n]^{-1}\right]^{-1}  \left[\sum_{n=0}^{N-1}{C}[n]^{-1}{x}[n]\right] $$

</div>
</div>
</div>
</div>