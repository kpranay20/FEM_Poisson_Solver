# Finite Element Formulation

This section presents the finite element formulation used to solve the Poisson equation in one and two dimensions. The formulation described here is independent of programming language and serves as the mathematical foundation for all implementations in this project.

---

## Strong Form

We consider the Poisson equation

$$
\nabla^2 u(\mathbf{x}) = f(\mathbf{x}), \quad \mathbf{x} \in \Omega
$$

subject to Dirichlet boundary conditions

$$
u(\mathbf{x}) = g(\mathbf{x}), \quad \mathbf{x} \in \partial \Omega
$$

where $$\Omega \subset \mathbb{R}^d$$, with $$d = 1, 2$$.


## Weak Formulation

To derive the weak form, we multiply the governing equation by a test function  
$$v \in V$$, where $$V$$ is a suitable function space satisfying homogeneous Dirichlet conditions, and integrate over the domain:

$$
\int_{\Omega} v \, \nabla^2 u \, d\Omega = \int_{\Omega} v f \, d\Omega
$$

Applying integration by parts and enforcing Dirichlet boundary conditions yields:

$$\int_{\Omega} \nabla v \cdot \nabla u \, d\Omega=\int_{\Omega} v f \, d\Omega$$

The weak problem is therefore:

> Find $$u \in V$$ such that  $$a(u, v) = l(v) \quad \forall v \in V$$ where, $$a(u, v) = \int_{\Omega} \nabla v \cdot \nabla u \, d\Omega$$ and $$l(v) = \int_{\Omega} v f \, d\Omega$$



## Finite Element Approximation

The solution $$u$$ is approximated using a finite-dimensional subspace $$V_h \subset V$$:

$$
u_h(\mathbf{x}) = \sum_{i=1}^{N} U_i \, \phi_i(\mathbf{x})
$$

where:
- $$\phi_i$$ are the basis (shape) functions,
- $$U_i$$ are the unknown nodal coefficients,
- $$N$$ is the number of degrees of freedom.

The same basis functions are used as test functions (Galerkin method).



## Discrete System

Substituting the finite element approximation into the weak form gives:

$$
\sum_{j=1}^{N} U_j \int_{\Omega} \nabla \phi_i \cdot \nabla \phi_j \, d\Omega=\int_{\Omega} \phi_i f \, d\Omega
$$

This results in the linear system:

$$
\mathbf{K} \mathbf{U} = \mathbf{F}
$$

where:
- $$K_{ij} = \int_{\Omega} \nabla \phi_i \cdot \nabla \phi_j \, d\Omega$$ is the global stiffness matrix,
- $$F_i = \int_{\Omega} \phi_i f \, d\Omega$$ is the global load vector.



## Element-Level Formulation

The global stiffness matrix and load vector are assembled from element-level contributions.

For each element $$e$$:

$$
K_{ij}^{(e)} = \int_{\Omega_e} \nabla \phi_i^{(e)} \cdot \nabla \phi_j^{(e)} \, d\Omega
$$

$$
F_i^{(e)} = \int_{\Omega_e} \phi_i^{(e)} f \, d\Omega
$$

Numerical quadrature is used to evaluate these integrals.


## One-Dimensional Elements

In one dimension, linear elements are used.

For an element with nodes $$x_1, x_2$$, the basis functions are:

$$
\phi_1(x) = \frac{x_2 - x}{h}, \quad
\phi_2(x) = \frac{x - x_1}{h}
$$

where $$h = x_2 - x_1$$.

The element stiffness matrix is:

$$
\mathbf{K}^{(e)} = \frac{1}{h}
\begin{bmatrix}
1 & -1 \\
-1 & 1
\end{bmatrix}
$$



## Two-Dimensional Elements

In two dimensions, the domain is discretized using structured quadrilateral elements or simplicial elements, depending on implementation.

For linear basis functions, the gradients of the shape functions are constant within each element, simplifying the evaluation of the stiffness matrix.

The general element stiffness matrix retains the form:

$$
K_{ij}^{(e)} = \int_{\Omega_e} \nabla \phi_i \cdot \nabla \phi_j \, d\Omega
$$

The specific form depends on the element geometry and mapping to the reference element.



## Assembly Procedure

The global system is assembled by summing element contributions:

1. Loop over elements
2. Compute local stiffness matrix and load vector
3. Map local degrees of freedom to global indices
4. Accumulate values into global matrix and vector

This procedure is identical across all implementations in this project, differing only in data structures and solvers.



## Boundary Conditions

Dirichlet boundary conditions are imposed by modifying the global system:

- Rows and columns corresponding to boundary nodes are adjusted
- Prescribed values are enforced directly

The exact enforcement strategy depends on the solver backend and is discussed in later sections.

