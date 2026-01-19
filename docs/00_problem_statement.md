# Problem Statement

## Governing Equation

We consider the Poisson equation

\[
\nabla^2 u(\mathbf{x}) = f(\mathbf{x}), \quad \mathbf{x} \in \Omega
\]

subject to Dirichlet boundary conditions

\[
u(\mathbf{x}) = g(\mathbf{x}), \quad \mathbf{x} \in \partial \Omega
\]

where:
- \( \Omega \subset \mathbb{R}^d \) is the computational domain (with \( d = 1, 2 \)),
- \( f(\mathbf{x}) \) is a prescribed source term,
- \( g(\mathbf{x}) \) specifies boundary values.

---

## Objective

The primary objective of this project is to **develop, verify, and scale a finite-element Poisson solver** through a progressive implementation strategy:

1. Establish correctness using simple CPU-based solvers.
2. Introduce GPU acceleration while preserving numerical equivalence.
3. Achieve parallel scalability using MPI and GPU-enabled linear solvers.

The emphasis is on **numerical correctness, reproducibility, and performance analysis**, rather than algorithmic novelty.

---

## Scope of the Study

This project focuses on:

- **Dimensionality**
  - 1D Poisson problem
  - 2D Poisson problem on structured grids

- **Numerical Method**
  - Finite Element Method (FEM)
  - Low-order basis functions
  - Explicit matrix assembly

- **Implementation Progression**
  1. Python (NumPy): CPU-based reference solver
  2. Python (CuPy): GPU-accelerated solver
  3. Fortran + LAPACK: Serial high-performance solver
  4. Fortran + PETSc: MPI-parallel and CUDA-enabled solver

---

## Motivation

The Poisson equation serves as a canonical elliptic PDE that appears in a wide range of physical problems, including electrostatics, heat conduction, and incompressible flow formulations.

Despite its apparent simplicity, efficient large-scale solutions require:
- Careful discretization,
- Robust linear solvers,
- Scalable parallel and GPU-aware implementations.

By solving the *same mathematical problem* across multiple programming models and hardware architectures, this project enables:
- Clear verification of numerical correctness,
- Isolation of performance bottlenecks,
- Direct comparison between CPU, GPU, and distributed solvers.

---

## Key Questions Addressed

This work aims to answer the following questions:

1. How does a basic FEM Poisson solver behave as problem size increases?
2. What performance gains are achievable using GPU acceleration alone?
3. How does PETSc manage data movement and computation for MPI + CUDA executions?
4. What limitations and anomalies arise in strong-scaling scenarios?

---

## Expected Outcomes

- Verified FEM solutions in 1D and 2D
- Consistent numerical results across Python and Fortran implementations
- Quantitative comparison of CPU vs GPU performance
- Analysis of parallel scalability using PETSc
- Identification of performance anomalies and hardware limitations

---

## Organization of the Documentation

The remainder of the documentation is organized as follows:

- **01_fem_formulation.md** — Weak form and finite element discretization
- **02_grid_discretization.md** — Mesh generation and indexing
- **03_python_cpu_implementation.md** — NumPy-based solver
- **04_python_gpu_cupy.md** — GPU acceleration using CuPy
- **05_fortran_serial_lapack.md** — Fortran serial solver
- **06_fortran_petsc_mpi_gpu.md** — MPI and CUDA-enabled PETSc solver
- **07_verification_validation.md** — Error norms and convergence
- **08_performance_analysis.md** — Timing, scaling, and PETSc logs
- **09_limitations_future_work.md** — Known issues and extensions

---
