---
layout: post
title: "Schur Complement Lemma and some Simple Applications"
author: "Kong Yao"
categories: journal
tags: [LMIs, robust control]
image: post2.jpg
---
This note elaborates on the Schur Complement Lemma and some of its applications in LMIs.

---

To start off, let's define what Schur complements are.

$\textbf{Definition 1}$: Given a partitioned matrix

$$
M =
\begin{bmatrix}
    A & B \\
    C & D \\
\end{bmatrix},
$$

If $A$ is nonsingular, $D - CA^{-1}B$ is the Schur complement of $A$ in $M$. 

Also, if $D$ is nonsingular, $A - BD^{-1}C$ is the Schur complement of $D$ in $M$.

---

$\textbf{Schur Complement Lemma}:$ Suppose $M$ is symmetric

$$
M =
\begin{bmatrix}
    A & B \\
    B^T & D \\
\end{bmatrix}.
$$

Then, 

$$
A \succ 0 \Leftrightarrow A \succ 0,\;\; D - B^{T}A^{-1}B \succ 0 \Leftrightarrow D \succ 0,\;\;A - BD^{-1}B^{T} \succ 0 $$  
or
$$
A \prec 0 \Leftrightarrow A \prec 0,\;\; D - B^{T}A^{-1}B \prec 0 \Leftrightarrow D \prec 0,\;\;A - BD^{-1}B^{T} \prec 0 $$. 

---
## Example 1

As an application of the Schur complement lemma, consider the following type of Riccati inequalities,

Let $A \in \mathbb{R}^{n\times n}, B \in \mathbb{R}^{n\times m}, C \in \mathbb{R}^{m\times n}, Q \in \mathbb{S}^n, R \in \mathbb{S}^m$ and suppose

$$
A^TP + PA - (PB+C^T)R^{-1}(B^TP+C)+Q \succ 0
$$


Here, we want to find a matrix $P$ that satisfies the above inequality. Utilizing the Schur Complement Lemma, this can be transformed into an linear matrix inequality (LMI) in $P$, which is computationally tractable and can be solved through convex optimization. By the lemma, if $R \succ 0$, then

$$
\begin{bmatrix}
    A^TP + PA + Q & PB+C^T \\
    B^TP + C & R \\
\end{bmatrix} \succ 0.
$$

---
## Example 2

The Schur Complement Lemma can also be used to formulate LMIs into their equivalent forms. Here's a theorem in $H_{\infty}$ control synthesis that state two equivalent LMIs that can be converted via the Schur complement Lemma,

$\textbf{Theorem 1}:$ Suppose $G(s) = C(sI - A)^{-1}B + D$. Then $||G(s)||_{\infty} \leq \gamma$ if and only if there exists $P \succ 0$ such that either of these inequalities holds:

$$
\begin{bmatrix}
    A^TP + PA & PB & C^T \\
    B^TP & -\gamma^2 I & D^T\\
    C & D & -I \\
\end{bmatrix} \prec 0,
$$

or 

$$
\begin{bmatrix}
    A^TP + PA + C^TC & PB+C^TD \\
    B^TP + D^TC & D^TD - \gamma^2 I \\
\end{bmatrix} \prec 0.
$$

To see the equivalence, re-write the second inequality as

$$
\begin{bmatrix}
    A^TP + PA & PB \\
    B^TP & -\gamma^2 I \\
\end{bmatrix} + 
\begin{bmatrix}
    C^T \\
    D^T \\
\end{bmatrix}
\begin{bmatrix}
    C & D \\
\end{bmatrix} \prec 0.
$$
and apply the Schur Complement Lemma.