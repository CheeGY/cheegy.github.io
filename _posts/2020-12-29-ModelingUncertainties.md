---
layout: post
title: "Modeling of Uncertainties"
author: "Kong Yao"
categories: journal
tags: [Linear systems]
image: post3.jpg
---
This note introduces stochastic models for discrete-time linear time-invariant (LTI) systems. In particular, explicit forms of the state and disturbance covariance functions are derived.

---

Consider a discrete-time LTI system,

$$
\begin{aligned}
x(k+1) &= Ax(k) + B \epsilon(k)\\
w(k) &= Cx(k) + \epsilon(k),
\end{aligned} \label{1}\tag{1}
$$

where it is assumed that all eigenvalues of $A$ lie strictly inside the unit circle (asymptotically stable) and $\epsilon(k)$ is assumed to be standard Gaussian noise with zero mean and covariance $R_{\epsilon}$ and the process is also assumed to be stationary.

---

Suppose $n > k$. Observe from \eqref{1} that 

$$
x(n) = A^{n-k} x(k) + F\,\textbf{col}\{\epsilon(k), \epsilon(k+1),\dots,\epsilon(n-1)\}, \label{2}\tag{2}
$$

for some matrix $F$. 

Hence, the state covariance at timestep $n$, $P_n$ can be represented using inner products

$$
\begin{aligned}
P_{n} &= \langle x(n), x(k) \rangle \\
    &= \langle A^{n-k} x(k) + F\,\textbf{col}\{\epsilon(k), \epsilon(k+1),\dots,\epsilon(n-1)\}, x(k) \rangle \\
    &= A^{n-k} \langle x(k), x(k) \rangle + 0 \\
    &= A^{n-k} P_k.
\end{aligned} \label{3}\tag{3}
$$

Furthermore, the state covariance at time $n+1$, denoted by $P_{n+1}$, can be written as

$$
\begin{aligned}
P_{n+1} :&= \langle x(n+1), x(n+1) \rangle\\
    &= \langle Ax(n) + B\epsilon(n), Ax(n) + B\epsilon(n) \rangle \\ 
    &= A \langle x(n), x(n) \rangle A^T + B \langle \epsilon(n), \epsilon(n) \rangle B^T\\ 
    &= A P_{n} A^T + B R_{\epsilon} B^T
\end{aligned} \label{4}\tag{4}
$$

This relates the propagation of the state covariance matrix with the process dynamics, in particular $A$ and $B$ and noise covariance $R_{\epsilon}$.

---

Next, we derive an expression for the output covariance matrix,

$$
\begin{aligned}
\text{Cov}(w(n),w(k)) :&= \langle w(n), w(k) \rangle \\
&= \langle Cx(n) + \epsilon(n), Cx(k) + \epsilon(k) \rangle \\
&= C \langle x(n), x(k) \rangle C^T + C \langle x(n), \epsilon(k) \rangle +\\
&\quad\;\; \langle \epsilon(n), x(k) \rangle C^T + \langle \epsilon(n), \epsilon(k) \rangle.
\end{aligned} \label{5}\tag{5}
$$


For $n > k$, $\langle \epsilon(n), x(k) \rangle = 0$ and $\langle \epsilon(n), \epsilon(k) \rangle = 0$. 

Therefore,

$$
\begin{aligned}
\text{Cov}(w(n),w(k)) :&= \langle w(n), w(k) \rangle \\
&= C \langle x(n), x(k) \rangle C^T + C \langle x(n), \epsilon(k) \rangle \\
&= CA^{n-k}P_k C^T +\\
&\quad\;\; C \langle A^{n-k-1} (Ax(k) + B\epsilon(k), \epsilon(k) \rangle\\
&= CA^{n-k-1}A P_k C^T + C A^{n-k-1}B \langle \epsilon(k), \epsilon(k) \rangle\\
&= CA^{n-k-1} \left( AP_kC^T + BR_{\epsilon}\right)\\
\end{aligned} \label{6}\tag{6}
$$

When $k,n \to \infty$, the state covariance $P_n$ from \eqref{2} reaches steady-state and it is a positive semi-definite matrix that satisfy the Lyapunov equation,

$$
P_n = A P_n A^T + B R_{\epsilon} B^T. \label{7}\tag{7}
$$