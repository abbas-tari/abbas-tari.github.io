---
title: An Optimal Image Packing Algorithm
tags: paper python go cpp java c#
image: static/content/pack/cover2.png
shortdesc: (2023) Optimally arranging and scaling 2D images on a canvas using constraint programming using OR-tools. The implementation is done in Python, Go, C++, Java, and C#.
---

<div class="justify-text">


# Python Implementation

## Optimizing Image Placement on a Canvas: A Dive into Rectangle Packing
Have you ever tried to efficiently arrange a collection of images on a canvas, attempting to minimize wasted space? It might seem like a simple challenge, but beneath the surface, it's a classic computational problem that's surprisingly intricate. I recently embarked on a journey to find an optimal arrangement for a set of images, and along the way, I learned about the deep history and complexity of this fascinating problem.

## A Historical Dilemma

While arranging images might seem mundane, it's a variant of the rectangle packing problem. Picture this: you have a collection of rectangular objects of varying dimensions, and your goal is to fit them inside a larger rectangle in a way that uses space efficiently. While this problem is prevalent in various industries, from logistics to textile manufacturing, it has a special place in the world of computer graphics. Game developers often need to pack textures into a single image, called a texture atlas, to reduce the number of draw calls and improve rendering performance.

But, there's a catch. This problem is not as easy as it first appears. In fact, it's known as an NP-hard problem. Without delving too deep into computational theory, NP-hard problems are those where no efficient solution exists, and solutions can take an incredibly long time to compute as the input size grows. Over the years, many algorithms have been proposed to tackle the rectangle packing problem. Each has its strengths and weaknesses, and none are perfect.

## Structure of the Solution: Two-Stage Optimization Problem
The main objective is to place a set of images optimally on a canvas such that the unused space is minimized. The solution uses two stages:

### Finding the optimal canvas size:
This involves a binary search approach to find a canvas size where all pictures fit without overlapping and the canvas is as square-like as possible.
If no solution is found for the current set of pictures, the largest picture is removed, and the process is repeated.
### Optimal placement of images on the canvas:
Here, we use a constraint programming approach to place the images on the canvas without overlapping.
Optionally, the images can be scaled to fit better and use less space.

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


<div>




## <span id="Resources">Resources</span>
Will be updated soon...!

<!-- <a class="arxiv-logo" href="https://arxiv.org/abs/2308.10097">Read or download the paper from</a>

<a class="github-logo" href="https://arxiv.org/abs/2308.10097">Github source code</a> -->

<!-- [Source Ccde]({{ site.url }}/static/content/rl/paper.pdf) -->


