---
layout: page
title: GatorPy
description: A Custom Implemented Linear Programming Solver. This project is a pure Python and NumPy implementation of Simplex Algorithm, Computational Math OOP, and LP Reductions.
img: assets/img/gatorpy_cover.jpg
importance: 10
category: 2025
project_intro: true
repository:
  - Hansespinosa2/ech4905-andres-espinosa
---

# GatorPy Report
GatorPy is an educationally motivated Linear Programming (LP) solver implemented in pure Python and NumPy. This project aims to demystify the internal workings of LP solvers by providing a simple, modular, and object-oriented framework. GatorPy transforms symbolic problem descriptions into slack form and solves them using the two-phase Simplex method.

See the below toy optimization example solved in GatorPy:

```python
# Parameters
A = Parameter(np.array([[1,1],[1.2,0.5]]))
b = Parameter(np.array([1,1]))
c = Parameter(np.array([1.2,1]))

# Variables
y = Variable(2)

# Problem
problem = Problem({
    'maximize': c.T @ y,
    'subject to': [
        A @ y <= b,
        y <= 1,
        y >= 0
    ]
})

solution = problem.solve()
print(solution)
print((1.14, [0.71, 0.29], True))
```
The GatorPy solver supports a custom modeling language (as seen above) and is designed to be readable, extensible, and transparent for other students and practicioners embarking on similar projects

View the full GatorPy report at 
<a href="../../assets/pdf/gatorpy_report.pdf">
this link 
</a>
