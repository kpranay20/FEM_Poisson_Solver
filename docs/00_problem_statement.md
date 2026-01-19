# Problem Statement

## Governing Equation

We consider the Poisson equation

$$\nabla^2 u(\mathbf{x}) = f(\mathbf{x}), \quad \mathbf{x} \in \Omega$$

subject to Dirichlet boundary conditions

$$
u(\mathbf{x}) = g(\mathbf{x}), \quad \mathbf{x} \in \partial \Omega
$$

where:
- $$\Omega \subset \mathbb{R}^d$$ is the computational domain with $$d = 1, 2$$,
- $$f(\mathbf{x})$$ is a prescribed source term,
- $$g(\mathbf{x})$$ specifies boundary values.



## Objective

The objective of this project is to develop, verify, and scale a finite element solver for the Poisson equation through a systematic progression of implementations:

1. Establish numerical correctness using CPU-based solvers.
2. Introduce GPU acceleration while preserving solution fidelity.
3. Achieve parallel scalability using MPI and GPU-enabled linear solvers.



## Scope of the Study

The scope of this work includes:

### Dimensionality
- One-dimensional Poisson problem
- Two-dimensional Poisson problem on structured grids

### Numerical Method
- Finite Element Method (FEM)
- Low-order basis functions
- Explicit global matrix assembly

### Implementation Progression
1. **Python (NumPy)**  
   CPU-based reference implementation for verification and debugging.

2. **Python (CuPy)**  
   GPU-accelerated implementation to assess raw GPU performance without MPI.

3. **Fortran + LAPACK**  
   High-performance serial solver for larger problem sizes.

4. **Fortran + PETSc (MPI + CUDA)**  
   Distributed-memory parallel solver with GPU acceleration.

Each implementation solves the **same mathematical problem**, done for comparison across architectures.



## Questions Addressed

This work aims to answer the following questions:

1. How does a basic FEM Poisson solver behave under mesh refinement?
2. What performance gains are achievable using GPU acceleration alone?
3. How does PETSc manage computation and data movement in MPI + CUDA executions?
4. What limitations or anomalies arise in strong-scaling studies?



## Expected Outcomes

The expected outcomes of this project are:

- Verified FEM solutions in 1D and 2D
- Consistent numerical results across Python and Fortran implementations
- Quantitative comparison of CPU and GPU performance
- Analysis of parallel scalability using PETSc
- Identification of performance limitations and hardware-related bottlenecks




