---
title: An Optimal Image Packing Algorithm
tags: paper python go cpp java c#
image: static/content/pack/solution_visualization.png
shortdesc: (2023) Optimally arranging and scaling 2D images on a canvas using constraint programming using OR-tools. The implementation is done in Python, Go, C++, Java, and C#.
---

<div class="justify-text">


# Python Implementation

## Optimizing Image Placement on a Canvas: A Dive into Rectangle Packing
Have you ever tried to efficiently arrange a collection of images on a canvas, attempting to minimize wasted space? It might seem like a simple challenge, but beneath the surface, it's a classic computational problem that's surprisingly intricate. I recently embarked on a journey to find an optimal arrangement for a set of images, and along the way, I learned about the deep history and complexity of this fascinating problem.

## A Historical Dilemma

While arranging images might seem mundane, it's a variant of the rectangle packing problem. Picture this: you have a collection of rectangular objects of varying dimensions, and your goal is to fit them inside a larger rectangle in a way that uses space efficiently. While this problem is prevalent in various industries, from logistics to textile manufacturing, it has a special place in the world of computer graphics. Game developers often need to pack textures into a single image, called a texture atlas, to reduce the number of draw calls and improve rendering performance.

But, there's a catch. This problem is not as easy as it first appears. In fact, it's known as an NP-hard problem. Without delving too deep into computational theory, NP-hard problems are those where no efficient solution exists, and solutions can take an incredibly long time to compute as the input size grows. Over the years, many algorithms have been proposed to tackle the rectangle packing problem. Each has its strengths and weaknesses, and none are perfect.

## Structure of the Solution: A Creative Twist on Two-Stage Optimization
When faced with the challenge of minimizing unused space while arranging images on a canvas, we might be tempted to think it's a straightforward problem. However, the solution I've developed adds a dash of ingenuity to this seemingly simple puzzle. It's a testament to how a creative approach can transform a complex problem into an engaging and solvable challenge.

### Finding the Optimal Canvas Size: Not Just Any Binary Search
The first stage of this journey uses a binary search method, but not in the way you might expect. This isn't your run-of-the-mill binary search; it's a clever adaptation that seeks the most 'square-like' canvas size. Why square-like? Because it often leads to the most aesthetically pleasing and space-efficient arrangements.

And here's where it gets interesting: if we hit a roadblock and can't fit all the pictures, we don't just give up. Instead, we take a step back, remove the largest picture, and try again. This iterative process, much like an artist trying different compositions, ensures we find a canvas size that's just right.
### Optimal Placement of Images on the Canvas: Constraint Programming with a Twist
The second stage is where constraint programming shines. But it's not just about avoiding overlaps; it's about doing so in a way that's both efficient and visually appealing. We're not merely cramming images onto a canvas; we're orchestrating their placement with precision.

What's more, we introduce the option of scaling images. This is not just scaling for the sake of it, but a strategic move to make the best use of available space. It’s akin to finding the perfect puzzle piece – sometimes a slight adjustment can make all the difference.

```python
def find_optimal_canvas(pictures, ...):
    ...
    return best_canvas_width, best_canvas_height, best_solution

def solve_optimal_arrangement(pictures, ...):
    ...
    return solution
```

## Tools Used: OR-Tools and its Solver
OR-Tools is Google's open-source software suite for optimization, which is utilized to solve the given constraint optimization problem.

`cp_model.CpModel()` creates an instance of the constraint programming model.
`cp_model.CpSolver()` is used to solve the defined model.

```python
from ortools.sat.python import cp_model
model = cp_model.CpModel()
solver = cp_model.CpSolver()

```

## Constraints and Objective Functions
### Constraints:
Image Boundaries: Ensure that images do not go outside the canvas boundary.
Non-overlapping: Images should not overlap each other.
Scaling: If scaling is allowed, images can be resized within a specified range.

```python
def add_non_overlapping_constraints(model, x, y, widths, heights):
    ...

def solve_optimal_arrangement(pictures, ...):
    ...
    # Constraints to make sure images are within canvas bounds
    for i in range(n):
        model.Add(x[i] + scaled_widths[i] <= canvas_width)
        model.Add(y[i] + scaled_heights[i] <= canvas_height)
    ...

```

### Objective Functions:
Unused Space: Minimize the unused space on the canvas.
Max Dimension: Minimize the maximum dimension of the bounding box containing all images.
Perimeter: Minimize the sum of the width and height of the bounding box containing all images.
Difference in Width and Height: Minimize the absolute difference between the width and height of the bounding box containing all images.

```python
def solve_optimal_arrangement(pictures, ...):
    ...
    # Selecting the objective function
    if objective_type == "unused_space":
        ...
    elif objective_type == "max_dimension":
        ...
    elif objective_type == "perimeter":
        ...
    elif objective_type == "diff_width_height":
        ...
    else:
        raise ValueError("Invalid objective_type.")
    ...

```

## Binary Search for Dimensions

In this approach, the size of the bounding box (or canvas) isn't decreased in fixed steps. Instead, a binary search technique is employed. This involves defining a range for the canvas dimensions and trying the midpoint size of this range. Depending on whether a solution is found with this size or not, the range of canvas dimensions is adjusted. This method is more efficient than simply reducing the size in fixed steps, as it can converge to the optimal size more quickly.

```python
def find_optimal_canvas(pictures, 
initial_canvas_width=INITIAL_CANVAS_WIDTH, initial_canvas_height=INITIAL_CANVAS_HEIGHT, objective_type="perimeter"):
    ...
    while canvas_width_low <= canvas_width_high and canvas_height_low <= canvas_height_high:
        canvas_width_mid = (canvas_width_low + canvas_width_high) // 2
        canvas_height_mid = (canvas_height_low + canvas_height_high) // 2
        ...

```

## Dynamic Adjustment of Alpha Range

Instead of using a fixed range for the alpha values (scaling factors for images), the range is dynamically adjusted based on the current bounding box size. The idea is to allow smaller scaling for larger bounding boxes and larger scaling for smaller bounding boxes.

```python
def adjust_alpha_range(picture: tuple, bounding_box_area: float, base_alpha_range: tuple = (BASE_ALPHA_MIN, BASE_ALPHA_MAX)):
    ...
    adjusted_alpha_min = base_alpha_range[0] + 10 * ((area_ratio > 0.8) - (area_ratio < 0.2))
    ...

```

## Initial Arrangement

Instead of starting with a random arrangement of images, a heuristic is used to determine an initial arrangement. This method sorts the images by their area in descending order, with the idea being that placing the largest images first might help the solver find a better solution more quickly.

```python
def optimized_initial_arrangement(pictures):
    ...
    # Sort the pictures in decreasing order based on their area (width x height)
    sorted_pictures = sorted(pictures, key=lambda pic: pic[0]*pic[1], reverse=True)
    return sorted_pictures
```

## Parallel Solving

OR-Tools provides capabilities to solve problems in parallel. This means that if you have a multi-core machine, you can use these capabilities to potentially find solutions faster by leveraging multiple CPU cores simultaneously.

```python
def solve_optimal_arrangement(pictures, ... , num_search_workers=8, ...):
    ...
    solver = cp_model.CpSolver()
    solver.parameters.num_search_workers = num_search_workers
    ...
```

## Results

The following image showcases the solution of the optimization problem. It represents the optimal placement of images on the canvas, achieved through the described methodologies. This visualization helps in understanding how the images are arranged to minimize unused space, adhering to the constraints and objective functions defined in the model.

<img src="{{ site.url }}/static/content/pack/solution_visualization.png" style="width:550px;height:auto;" alt="Image description" />

## Optimization Log Summary

```html
Using initial picture dimensions: : [(3133, 2126), (2532, 721), (2983, 2156), (961, 640), (980, 1132), (3149, 2102)]
Initial canvas size:           : 8000x8000 
Optimized picture arrangement: : [(3133, 2126), (3149, 2102), (2983, 2156), (2532, 721), (980, 1132), (961, 640)]
Trying canvas dimensions:      : 4480x4320. Solution found: No
Trying canvas dimensions:      : 6240x4320. Solution found: Yes
Trying canvas dimensions:      : 5360x4320. Solution found: No
Trying canvas dimensions:      : 5800x4320. Solution found: No
Trying canvas dimensions:      : 6020x4320. Solution found: No
Trying canvas dimensions:      : 6130x4320. Solution found: Yes
Trying canvas dimensions:      : 6075x4320. Solution found: No
Trying canvas dimensions:      : 6102x4320. Solution found: No
Trying canvas dimensions:      : 6116x4320. Solution found: Yes
Trying canvas dimensions:      : 6109x4320. Solution found: No
Trying canvas dimensions:      : 6112x4320. Solution found: No
Trying canvas dimensions:      : 6114x4320. Solution found: No
Trying canvas dimensions:      : 6115x4320. Solution found: No
Optimal canvas dimensions:     : 6116x4320 
Adjusted Alpha Below Minimum for Image Size : 2532x721  
Area Ratio                     : 0.07      
Adjusted Alpha Range           : (70, 150) 
Bounding Box Area              : 26421120  
Adjusted Alpha Below Minimum for Image Size : 980x1132  
Area Ratio                     : 0.04      
Adjusted Alpha Range           : (70, 150) 
Bounding Box Area              : 26421120  
Adjusted Alpha Below Minimum for Image Size : 961x640   
Area Ratio                     : 0.02      
Adjusted Alpha Range           : (70, 150) 
Bounding Box Area              : 26421120  
Alpha/Scaling factor for Image 0 : 100%      
Alpha/Scaling factor for Image 1 : 104%      
Alpha/Scaling factor for Image 2 : 99%       
Alpha/Scaling factor for Image 3 : 112%      
Alpha/Scaling factor for Image 4 : 122%      
Alpha/Scaling factor for Image 5 : 150%  
```
<div>




## <span id="Resources">Resources</span>

<!-- <a class="arxiv-logo" href="https://arxiv.org/abs/2308.10097">Read or download the paper from</a> -->

<a class="github-logo" href="https://github.com/abbas-tari/2d-packing-optimization">Github source code [Python]</a>

<!-- [Source Ccde]({{ site.url }}/static/content/rl/paper.pdf) -->


