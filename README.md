# HyperbolicEmbeddings

# README.md for Hyperbolic Laplacian Experimentation

## Overview

This document serves as a guide for the Jupyter notebook containing several key classes and methods related to the exploration and application of the hyperbolic Laplacian in graph theory. The notebook focuses precisely on decision trees, examining how (ultra-)hyperbolic geometry can be applied to graph analysis and embedding.

## Classes

### 1. `Tree`

#### Description

The basic tree-wrapping class made for convenience of use, when dealing with `sklearn` decision trees. Takes two parameters at initialization: `tree` and `make_adj_matrix`, the latter of which is a conditional statement to create an adjacency matrix at initialization.

#### Instances

- `__tree`: A `sklearn.tree._tree.Tree` Decision tree structure, stored at initialization.
- `__adj_matrix`: Upper triangular adjacency matrix for the given `__tree` instance. (optional)
- `node_count`: Public instance describing the number of nodes in a tree.

#### Methods

- `adjacency_matrix(sparse=True) -> None` : Creates an adjacency matrix for the given tree in CSR format if `sparse=True`.
- `get_tree -> sklearn.Tree`: Returns the tree.
- `get_adj_matrix(sparse=True) -> np.ndarray or sps.csr_matrix`: Returns the adjacency matrix of the tree in CSR format if `sparse=True`.

### 2. `Embedding`

#### Description

Class which is devoted to creating a space-specific embedding of a given tree. At initialization takes parameters:
- `tree`: A `Tree` class object.
- `space_type='Euclidean`: Space type to be used during the embedding procedure. Has to be either `Euclidean` (default) or `Hyperbolic` (optional).
- `alphas=None`: An array of alpha values for the hyperbolic laplacian, by default set to `None`.

#### Instances

- `__space_type`: The space type provided at initialization.
- `__tree`: The tree provided at initialization.
- `tree_adj_mat`: Public instance holding adjacency matrix of the provided tree.
- `__alphas`: An array of alphas either provided at initialization or initialized by default.
- `__lap`: Laplacian of the given tree, defined in `__space_type` space.
- `__eigvals`: An array of eigenvalues of the laplacian of the tree.
- `__eigvecs`: A multidimensional array with eigenvectors of the laplacian as columns

#### Methods

- `make_eigenmaps(embed_dim, normed=False, symmetrized=True) -> None`: Computes the eigenvalues and eigenvectors of the Laplacian matrix in the given space for the provided tree. This function is used for embedding graphs in a lower-dimensional space. The subspace's dimension to be used is `embed_dim`. `normed` is a boolean flag to determine whether to use a normalized Laplacian (configurable). `symmetrized` is the boolean flag that is `True` by default, used to symmetrize the adjacency matrix, which is by default upper traingular. Sets `__lap`, `__eigvals` and `__eigvecs` instances.
- `get_eigenmaps(embed_dim, normed=False, symmetrized=True) -> Tuple[np.ndarray, np.ndarray]`: Method that returns the eigenvalues and the eigenvectors for the provided tree as a tuple of two multidimensional arrays. Arguments serve the same purpose as in `make_eigenmaps` method.
- `get_laplacian(embed_dim, normed=False, symmetrized=True, sparse=True) -> np.ndarray or sps.csr_matrix`: Method that returns the laplacian of the given tree in the considered space. Arguments serve the same purpose as in `make_eigenmaps` method, the only difference is `sparse` boolean flag, which determines if the returned laplacian is in sparse or dense format.
- `plot_eigen_dependency(idx_1, idx_2, title)`: Visualizes the graph by plotting the nodes using the two different eigenvectors and drawing edges according to the adjacency matrix. `idx_1` stands for the index of the first eigenvector to consider, `idx_2` stands for the index of the second eigenvector to consider. `title` sets the title of the correspoding graph of dependencies (optional).



## Functions

### 1. `project_vertices(eigvecs)` (has not been used during the main experiment)

- **Description**: Creates a projection of the eigenmap onto a 2D surface, using the first three eigenvectors as support.
- **Input**:
  - `eigvecs`: A multidimensional array with eigenvectors of the Laplacian as columns.
- **Output**: 
  - A tuple of arrays, representing the projected x and y coordinates of the vertices, encoded in eigenvectoes.

## Usage

To use all the named classes and methods in the notebook:

1. Ensure that all necessary dependencies, such as `numpy`, `scipy`, `sklearn`, `seaborn` and `matplotlib`, are installed.
2. Import the named classes and functions into your Jupyter notebook.
3. Utilize these classes and methods as part of your analysis and experimentation with decision trees and hyperbolic Laplacian applications in graph theory.

## Conclusion
