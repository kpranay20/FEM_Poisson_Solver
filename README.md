# Finite Element Solution of the Poisson Equation  
### From CPU Prototypes to MPI + GPU Acceleration

## Overview

This repository documents the progressive development of a **finite element solver for the Poisson equation**, starting from simple CPU-based implementations and extending to parallel, GPU-accelerated solvers using PETSc.

The same mathematical problem is solved across multiple programming languages and hardware architectures in order to:
- verify numerical correctness,
- study performance scaling,
- and understand the practical challenges of MPI and GPU-enabled solvers.



## Problem Description

We consider the Poisson equation

$$\nabla^2 u(\mathbf{x}) = f(\mathbf{x})$$

on one- and two-dimensional domains with Dirichlet boundary conditions.

The problem is discretized using the **finite element method (FEM)** with low-order basis functions and explicit matrix assembly.

Full mathematical formulation and discretization details are provided in the documentation.



## Implementation Workflow

The solver is developed in a staged manner:

1. **Python (NumPy, CPU)**
   - Reference implementation
   - Verification and debugging
   - Grid convergence studies

2. **Python (CuPy, GPU)**
   - Direct GPU acceleration of the FEM solver
   - Assessment of GPU performance without MPI

3. **Fortran + LAPACK (CPU)**
   - High-performance serial solver
   - Numerical equivalence with Python implementations

4. **Fortran + PETSc (MPI + CUDA)**
   - Distributed memory parallelism
   - GPU-enabled sparse linear solvers
   - Strong scaling and performance analysis

Each stage solves the *same mathematical problem* to ensure consistency and traceability.



## Repository Structure

```text
poisson-fem/
│
├── README.md
├── docs/
│   ├── 00_problem_statement.md
│   ├── 01_fem_formulation.md
│   ├── 02_grid_discretization.md
│   ├── 03_python_cpu_implementation.md
│   ├── 04_python_gpu_cupy.md
│   ├── 05_fortran_serial_lapack.md
│   ├── 06_fortran_petsc_mpi_gpu.md
│   ├── 07_verification_validation.md
│   ├── 08_performance_analysis.md
│   └── 09_limitations_future_work.md
│
├── python/
│   ├── poisson_1d_cpu.py
│   ├── poisson_2d_cpu.py
│   ├── poisson_2d_cupy.py
│   └── mesh_utils.py
│
├── fortran/
│   ├── poisson_1d_lapack.f90
│   ├── poisson_2d_lapack.f90
│   ├── poisson_2d_petsc.f90
│   └── Makefile
│
├── scripts/
│   ├── run_python_cpu.sh
│   ├── run_python_gpu.sh
│   ├── run_petsc_cpu.sh
│   ├── run_petsc_gpu.sh
│
├── results/
│   ├── figures/
│   ├── timings/
│   └── petsc_logs/
│
└── environment/
    ├── requirements.txt
    ├── cuda_info.txt
    └── petsc_config.txt
```

## Acknowledgments

This README was created with the help of ChatGPT. All technical content, implementation details and project decisions remain my own.
