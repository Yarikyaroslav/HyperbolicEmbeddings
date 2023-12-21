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

- `make_eigenmaps(embed_dim, normed=False, symmetrized=True)`: Computes the eigenvalues and eigenvectors of the Laplacian matrix in the given space for the provided tree. This function is used for embedding graphs in a lower-dimensional space. The subspace's dimension to be used is `embed_dim`. `normed` is a boolean flag to determine whether to use a normalized Laplacian (configurable). `symmetrized`



## Functions Included

### 1. `create_adjacency_matrix(tree)`

- **Description**: Constructs an adjacency matrix in Compressed Sparse Row (CSR) format from a given decision tree.
- **Input**:
  - `tree`: A decision tree structure, typically obtained from a trained decision tree model.
- **Output**: 
  - A CSR matrix representing the adjacency matrix of the tree.

### 2. `laplacian_eigenmaps(adjacency_matrix, embed_dim, norm_laplacian=False)`
- This function originates from the seminars.
- **Description**: Computes the eigenvalues and eigenvectors of the Laplacian matrix for a given adjacency matrix. This function is used for embedding graphs in a lower-dimensional space.
- **Inputs**:
  - `adjacency_matrix`: The adjacency matrix of the graph in CSR format.
  - `embed_dim`: The embedding dimension, determining the number of eigenvalues and eigenvectors to compute.
  - `norm_laplacian`: A boolean flag to determine whether to use a normalized Laplacian.
- **Output**: 
  - A tuple of eigenvalues and eigenvectors.

### 3. `plot_graph_with_edges(eigvec1, eigvec2, adjacency_matrix, title='Graph with Edges')`

- **Description**: Visualizes the graph by plotting the nodes using the two different eigenvectors and drawing edges according to the adjacency matrix.
- **Inputs**:
  - `eigvec1`, `eigvec2`: Different eigenvectors for plotting the nodes in 2D.
  - `adjacency_matrix`: The adjacency matrix of the graph.
  - `title` (optional): The title for the plot.
- **Output**: 
  - A plot of the graph with nodes and edges, saved as a PNG file.

### 4. `hyperbolic_laplacian(adjacency_matrix, alpha)`

- **Description**: Creates a hyperbolic Laplacian matrix for a given graph represented by its adjacency matrix and a vector of alpha values.
- **Inputs**:
  - `adjacency_matrix`: The adjacency matrix of the graph in CSR format.
  - `alpha`: A vector of alpha values.
- **Output**: 
  - The hyperbolic Laplacian matrix in CSR format.

### 5. `hyperbolic_laplacian_eigenmaps(adjacency_matrix, alpha, embed_dim)`

- **Description**: Computes the eigenvalues and eigenvectors of the hyperbolic Laplacian matrix, which is useful for hyperbolic embeddings of the graph.
- **Inputs**:
  - `adjacency_matrix`: The adjacency matrix of the graph in CSR format.
  - `alpha`: A 1D numpy array of alpha values for the hyperbolic Laplacian.
  - `embed_dim`: The embedding dimension for the eigenvalue and eigenvector computation.
- **Output**: 
  - A tuple of eigenvalues and eigenvectors of the hyperbolic Laplacian matrix.

## Usage

To use these functions in the notebook:

1. Ensure that all necessary dependencies, such as `numpy`, `scipy`, and `matplotlib`, are installed.
2. Import the functions into your Jupyter notebook.
3. Utilize these functions as part of your analysis and experimentation with decision trees and hyperbolic Laplacian applications in graph theory.

## Conclusion
