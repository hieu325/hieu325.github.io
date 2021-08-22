---
layout: page
title: wave propagation
description: Developing a stable parallel-in-time scheme for the wave equation
img: /assets/img/wave.png
#importance: 1
#category: work
---

In many engineering applications, scientists use wave signals to image 
regions are often much larger than the signal wavelength, which makes the simulation challenging
due to the numerical stability constraint on spatial and temporal resolution.

Nowaday, large scale simulations are possible because of powerful supercomputers.
Such development makes parallel-friendly algorithms more favorable in many engineering simulations
than sequential algorithms. A successful example of the parallel algorithms is the domain decomposition approach.
This approach involves dividing the space domain into subdomains, each of which is sent to different computers
to solve. Once dividing into more subdomains does not give further speed-up, 
the decomposition in the time domain will be the key for concurrency.

Another reason for considering the parallel-in-time approach is the multiscale nature of
the high-frequency wave propagation in complicated media. At the microscale level,
we have a direct solver such as the finite difference time domain, which fully resolves
the wavefield and the medium. The direct solver is computationally expensive. 
Meanwhile, at the macroscale level, we have a coarser direct solver,
which efficiently approximates the wavefield solution. Through the parallel-in-time approach,
we systematically combine the solvers at the microscale and macroscale levels to obtain
high-fidelity wavefield in shorter wall-clock time.  

we proposed a data-driven parareal scheme. The original parareal scheme for PDE was developed by J. Lions, Y. Maday, G. Turinici. 
Concretely, the solution at n-th time step after \\(k\\) iterations can be written as

$$u^{k}_{n} = \theta^{k-1} \mathcal{G} u^{k}_{n-1} + 
\mathcal{F} u^{k-1}_{n-1} - \theta^{k-1} \mathcal{G} u^{k-1}_{n-1}$$
    
where \\(\mathcal{G},\mathcal{F}\\) denote the coarse and fine solver respectively.
The key idea is to gather previously computed solutions to construct an interpolator \\(\theta^{k}\\),
or correction operator, which is used to improve the accuracy of the coarse solver. 
It is crucial to consider the conservation of wave energy.
we convert the wavefield data into energy components so that the solution of a minimization problem
with orthogonality constraint is the correction operator. 
The minimization problem is in the form of the Procrustes problem, 
which is solved by the singular value decomposition method. 
After every iteration, the minimizer is updated by the low-rank QR factorization. 
For wave propagation in complex 2-D media, the numerical results show that the new scheme
is convergent and stable. 

Furthermore, in light of deep learning we train the correction operator in a supervised manner. 
The resulting \\(\theta\\)-parareal scheme becomes more robust to complicated medium heterogeneity.

<!--
Every project has a beautiful feature showcase page.
It's easy to include images in a flexible 3-column grid format.
Make your photos 1/3, 2/3, or full width.

To give your project a background in the portfolio page, just add the img tag to the front matter like so:

    ---
    layout: page
    title: project
    description: a project with a background image
    img: /assets/img/12.jpg
    ---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/1.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/3.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/5.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/5.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal it's glory in the next row of images.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/6.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/11.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/" target="_blank">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/6.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/11.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
```
-->
