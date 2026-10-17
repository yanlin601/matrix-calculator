# Matrix Calculator

A matrix calculator in Python, about 400 lines, that goes from basic operations up to eigendecomposition. I wrote it to practice linear algebra by coding the algorithms we learn in class. Almost everything is written by hand. The one exception is the root-finding step for eigenvalues, which uses NumPy's QR.

## Usage

Create a matrix with the `matrix` class, and use its methods to do the work:

```python
a = matrix([[0.46549264805211044, 0.5486606474663042],
            [0.568240454724809, 0.3130538544120218]])

s, l, s1 = a.eigendecomp()
abc = s * l * s1
```

`eigendecomp()` gives back three matrices. Multiplying them back together should reproduce `a`, which is how I checked that it works. The other operations are methods in the same way, for example `a.inverse()` and `a.eigvals()`.

## What it can do

- Basic matrix operations
- Determinant
- Inverse
- Eigenvalues
- Eigenvectors and eigendecomposition

## How it works

I used the standard algorithms from class.

**Inverse:** put the matrix next to the identity, as [A | I], and row reduce.

**Determinant:** cofactor expansion, which is O(n!). It's slow, but I did that on purpose so the determinant wouldn't reuse my row reduction code.

**Eigenvalues:** I wrote a `Polynomial` class. To get the characteristic polynomial, I subtract lambda from the main diagonal and take the determinant, the same way we do it by hand. The roots of that polynomial are the eigenvalues. I find the roots with NumPy's QR, since I didn't implement the QR algorithm myself.

**Eigenvectors:** solved for each eigenvalue the usual way from class.

## Requirements

Python 3 and NumPy, which is only used for finding polynomial roots.

## Limitations and next steps

Because the determinant is O(n!), the calculator is only practical for small matrices. If I come back to it, I'd like to write my own QR algorithm so it doesn't depend on NumPy, and switch the determinant to use row reduction.
