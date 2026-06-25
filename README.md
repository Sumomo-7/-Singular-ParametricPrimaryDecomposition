# Parametric Primary Decomposition
This repository provides a `SINGULAR` implementation of algorithms for computing a *comprehensive primary decomposition system* of a parametric polynomial ideal using generic Groebner bases.

The project is currently under active development. The implementation may change significantly between versions, and some functionalities may still be experimental. Updates, improvements, and bug fixes will be released as the project evolves.

## Overview

**`paraprimdec(F, Paras, Vars, Indet, RingVar, RingAll, [, q])`**\
The main function of the library. `paraprimdec` computes a comprehensive primary decomposition system of the parametric polynomial ideal $\langle F \rangle \subseteq \mathbb{Q}[A][X]$. \

**Given**
- `F`: finite set of $\mathbb{Q}[A][X]$,
- `Paras`: list of paramters,
- `Vars`: list of variables,
- `Indet`: list of all indeterminant,
- `RingVar`: polynomial ring where only elements of `Vars` are considered as variables while elements of `Paras` are used for transcendental extension,
- `RingAll`: polynomial ring where both elements of `Vars` and `Paras` considered as variables,
- `q`(optional): if specified, computations are performed over the finite field $\mathbb{F}_q$, if `q` is omitted, all computations are performed over the field of rational numbers $\mathbb Q$.
>[!WARNING] Finite field computations are currently experimental and have not been thoroughly tested. Results over $\mathbb{F}_q$ should therefore be used with caution.

**Find**

`[[[[Q_{11}, P_{11}], ..., [Q_{1r_1}, P_{1r_1}]], E_1, N_1, T_1], ..., [[[Q_{s1}, P_{s1}], ..., [Q_{sr_s}, P_{sr_s}]], E_s, N_s, T_s]]`, where
- `[[Q_{i1}, P_{i1}], ..., [Q_{ir_i}$, P_{ir_i}]]`: a list of pairs of primary ideal $Q_{ij}$ of $\mathbb Q[A][X]$ and its asscociated prime, as well as its radical $P_{ij}$,
- `E_i`: ideal of $\mathbb Q[A]$,
- `N_i`: list of polynomials of $\mathbb Q[A]$,
- `T_i`: list of irreducible polynomials of $mathbb Q[A][X]$, 
such that for parameter values $\alpha \in \mathbb{V}(E_i) \setminus \mathbb{V}(\prod_{g \in N_i}h)$, if for ever polynomial $f(A, X)$ of $T_i$, the specialized polynomial $\sigma_\alpha(f) = f(\alpha, X)$ is irrducible on $\mathbb{Q}[X]$, then $\{\sigma_\alpha(Q_{i1}), \ldots, \sigma_\alpha(Q_{ir_i})\}$ is a primary decomposition of the ideal $\langle \sigma_\alpha(F) \rangle$ ($i = 1, \ldots, s$).

## Example

```C++:singular
LIB "path/to/PARAprimdec.lib";
option(redSB);
option(noredefine);

ring RingAll = 0, (x, y, a, b), (lp(2), lp);
ring RingVar = (0, a, b), (x, y), lp;
ideal F = x2 - a, bxy;
list Paras = a, b;
list Vars = x, y;
list Indet = x, y, a, b;

paraprimdec(F, Paras, Vars, Indet, RingVar, RingAll);

[1]:
   [1]:
      [1]:
         [1]:
            _[1]=y
            _[2]=x2+(-a)
         [2]:
            _[1]=y
            _[2]=x2+(-a)
   [2]:
      _[1]=0
   [3]:
      [1]:
         (a)
      [2]:
         (b)
   [4]:
      [1]:
         x2+(-a)
[2]:
   [1]:
      [1]:
         [1]:
            _[1]=x
         [2]:
            _[1]=x
      [2]:
         [1]:
            _[1]=y
            _[2]=x2
         [2]:
            _[1]=y
            _[2]=x
   [2]:
      _[1]=(a)
   [3]:
      [1]:
         (b)
   [4]:
      [1]:
         1
[3]:
   [1]:
      [1]:
         [1]:
            _[1]=x2
         [2]:
            _[1]=x
   [2]:
      _[1]=(b)
      _[2]=(a)
   [3]:
      [1]:
         1
   [4]:
      [1]:
         1
[4]:
   [1]:
      [1]:
         [1]:
            _[1]=x2
         [2]:
            _[1]=x
   [2]:
      _[1]=(b)
      _[2]=(a)
   [3]:
      [1]:
         1
   [4]:
      [1]:
         1
[5]:
   [1]:
      [1]:
         [1]:
            _[1]=x2+(-a)
         [2]:
            _[1]=x2+(-a)
   [2]:
      _[1]=(b)
   [3]:
      [1]:
         1
   [4]:
      [1]:
         x2+(-a)
```


## Installation
This package consists of a single Singular library file, `PARAprimdec.lib`.

Download `PARAprimdec.lib` from this repository and load it into Singular by executing
```
singular LIB "path/to/PARAprimdec.lib"; 
```
where path/to/ should be replaced by the actual location of the file on your system.

After the library has been loaded successfully, all procedures provided by the package become available in the current Singular session.
