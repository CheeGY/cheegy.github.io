---
layout: post
title: "(Book) Robust Nonlinear Control Design: Introduction, Part II"
author: "Kong Yao"
categories: posts
tags:
- robust control
- nonlinear control
image: post6.jpg
---
This is a continuation of the presentation of key ideas from Chapter 1 of the book, "Robust Nonlinear Control Design", by R. Freeman and P. Kokotovic. For each idea/concept presented, references are stated explicitly (titles, authors etc.). This is to facilitate referencing and search in the future.

---

## Lyapunov Framework for Robust Control (cont'd)

Given a robust control problem, the next step is to find necessary and sufficient conditions for the stability of its solution. In the context of nonlinear systems, this corresponds to the existence of a Lyapunov function. Not only does Lyapunov functions guarantee stability of these systems, they also act as useful design tools.  In particular, control Lyapunov functions achieve this purpose. A control Laypunov function for the system $\dot{x} = f(x,u)$ is given as a candidate Lyapunov function $V(x)$ such that for every fixed $x$, there exists an admissible $u$ satisfying 

$$
\nabla V(x) \dot{x} = \nabla V(x) \cdot f(x,u) < 0.
$$ 

If $f$ is continuous and if there exist a continuous state feedback control law such that $x=0$ is globally asympotically stable, then by converse Lyapunov theorems, there exist such a control Lyapunov function. Furthermore, if $f$ is affine in $u$, then having a control Lyapunov function is sufficient for stabilizability for continuous state feedback.

### Control Lyapunov functions and related stability results
- Z. Artstein, _Stabilization with relaxed controls_, Nonlinear Anal., 7 (1983), pp. 1163-1173. 
- E. D. Sontag, _A Lyapunov-like characterization of asymptotic controllability_, SIAM J. Contr. Optimiz., 21 (1983), pp. 462-471
- E. D. Sontag, _A 'universal' construction of Artstein's theorem on nonlinear stabilization_, Syst. Contr. Lett., 13 (1989), pp. 117-123. 

However, in the case of robust nonlinear control, a control Lyapunov function is inadequate because:
- There are two input sources from the controller $K$ and uncertainty $\Delta$
- Control Lyapunov functions applies to state feedback only

Hence, the authors introduce the concept of a **robust control Lyaunov function**, which also generalizes output control Lyaunov functions. With this idea, two key design questions arise:
- Construction of robust control Lyaunov function for nonlinear systems (Chapters 5-8)
- Design of robust controller from robust control Lyaunov functions (Chapter 4)

---

## Inverse Optimality in Robust Stabilization

For a general nonlinear system $\dot{x} = f(x,u)$ and cost functional $J = \int_0^{\infty} L(x,u) dt$, getting the optimal solution with respect to the dynamics and cost involves solving a steady-state Hamilton-Jacobi-Isaacs (HJI) partial differential equation, i.e.,

$$
min_u max_w \left[ L(x,u) + \nabla V(x) \cdot f(x,u,w) \right] = 0,
$$

where $w$ is the uncertainty and the unknown variable is $V(x)$, also known as the value function. Appropriate choices of $L(x,u)$ lies to smooth, positive definite solutions $V(x)$ and optimal, robust state feedback control laws $u(x)$.

However, this is often difficult to compute. Looking from another perspective, if we can find a meaningful cost functional such that the given robust control Lyapunov function is its value function, then the control law would also inherit the benefits of optimality. This approach is known as an _inverse_ optimal robust stabilization problem. Inverse problems are long standing in optimal control and references can be found here:

### Inverse problems in optimal control
**LTI systems**
- R. E. Kalman, _When is a linear control system optimal?_, Trans. ASME Set. D: J. Basic Eng., 86 (1964), pp. 1-10. 
- B. D. O. Anderson AND J. B. Moore, _Linear Optimal Control_, Prentice-Hall, Englewood Cliffs, New Jersey, 1971.
- B. P. Molinari, _The stable regulator problem and its inverse_, IEEE Trans. Automat. Contr., 18 (1973), pp. 454-459. 

**Nonlinear systems**
- D. H. Jacoson, _Extensions of Linear-Quadratic Contol_, Optimization and Matrix Theory, Academic Press, London, 1977. 
- D. H. Jacoson, D. H. Martin, M. Pachter, and T. Geveci, _Extensions of Linear-Quadratic Contol Theory_, vol. 27 of Lecture Notes in Control and Information Sciences, SpringerVerlag, Berlin, 1980. 
- S. T. Glad, _Robustness of nonlinear state feedback - A survey_, Automatica, 23 (1987), pp. 425-435. 
- P. J. Moylan AND B. D. O. Anderson, _Nonlinear regulator theory and an inverse optimal control problem_, IEEE Trails. Automat. Contr., 18 (1973), pp. 460-464. 
- P. J. Moylan, Implications of passivity in a class of nonlinear systems, IEEE Trans. Automat. Contr., 19 (1974), pp. 373-381.
- C. A. Harvey AND G. Stein, _Quadratic weights for asymptotic regulator properties_, IEEE Trans. Automat. Contr., 23 (1978), pp. 378-387. 

**Homogenous systems**
- H. Hermes, _Asymptotically stabilizing feedback controls_, J. Differential Equations, 92 (1991), pp. 76-89. 
- H. Hermes, _Asymptotically stabilizing feedback controls and the nonlinear regulator problem_, SIAM J. Contr. Optimiz., 29 (1991), pp. 185-196. 

In this book, the approach to solve this inverse problem is to pose it as a two-person zero-sum differential game, referenced from
- T. Basar AND G. J. Olsder, _Dynamic Noncooperative Game Theory_, Academic Press, London, 1982. 

---

## Recursive Lyapunov Design

In Lyapunov redesign or min-max design, a control Lyapunov function is used as the robust control Lyapunov function under a set of matching conditions, which requires uncertainties to enter the system through the same channels as the control variables.

### Lyapunov redesign or min-max design (also see Guaranteed stability in Part I)
- H. K. Khalil, _Nonlinear Systems, Prentice Hall, Upper Saddle River, New Jersey, second ed., 1996. 
- M. W. Spong AND M. Vidyasagar, _Robot Dynamics and Control_, John Wiley & Sons, New York, 1989. 

These matching conditions are quite restrictive and hence, there exist articles that discuss the weakening of these conditions,
- J. S. Thorp AND B. R. Barmish, _On guaranteed stability of uncertain linear systems via linear control_, J. Optimiz. Theory Appl., 35 (1981), pp. 559-579. 
- B. R. Barmish AND G. Leitmann, _On ultimate boundedness control of uncertain systems in the absence of matching conditions_, IEEE Trans. Automat. Contr., 27 (1982), pp. 153-158. 
- Y. H. Chen AND G. Leitmann, _Robustness of uncertain systems in the absence of matching assumptions_, Int. J. Contr., 45 (1987), pp. 1527-1542. 
- K. Wei, _Quadratic stabilizability of linear systems with structural independent time-varying uncertainties, IEEE Trans. Automat. Contr., 35 (1990), pp. 268-277. 

Additional reference on a nonlinear stabilization technique of "adding an integrator",
- E. D. Sontag AND H. J. Sussmann, _Further comments on the stabilizability of the angular velocity of a rigid body, Syst. Contr. Lett., 12 (1988), pp. 213-217. 
- C. I. Byrnes AND A. Isidori, _New results and examples in nonlinear feedback stabilization_, Syst. Contr. Lett., 12 (1989), pp. 437-442. 
- J. Tsinias, _Sufficient Lyapunov-like conditions for stabilization_, Math. Control Signals Systems, 2 (1989), pp. 343-357. 

and its recursive form, also known as integrator backstepping, or simply backstepping,
- I. Kanellakopoulos, P. V. Kokotovic, and A. S. Morse, _Systematic design of adaptive controllers for feedback linearizable systems_, IEEE Trans. Automat. Contr., 36 (1991), pp. 1241-1253. 
- I. Kanellakopoulos, P. V. Kokotovic, and A. S. Morse, _A toolkit for nonlinear feedback design_, Syst. Contr. Lett., 18 (1992), pp. 83-92. 
- P. V. Kokotovic, _The joy of feedback: Nonlinear and adaptive_, IEEE Control Systems Magazine, 12 (1992), pp. 7-17. 
- M. Krstic, I. Kanellakopoulos, AND P. V. Kokotovic, _Nonlinear and Adaptive Control Design_, John Wiley & Sons, New York, 1995. 

For the nonlinear robust control problem formulated in this book, backstepping leads to a structural strict feedback condition, under which a robust control Lyapunov function can be constructed systematically. References for this robust form of backstepping can be found in
- R. A. Freeman AND P. V. Kokotovic, _Backstepping design of robust controllers for a class of nonlinear systems_, in Proceedings of the IFAC Nonlinear Control Systems Design Symposium, Bordeaux, France, June 1992, pp. 307-312. 
- R. Marino AND P. Tomei, _Robust stabilization or feedback linearizable time-varying uncertain nonlinear systems_, Automatica, 29 (1993), pp. 181-189. 
- R. Marino AND P. Tomei, _Nonlinear Control Design: Geometric, Adaptive, and Robust_, Prentice Hall, London, 1995.
- Y. H. Chen AND G. Leitmann, _Robustness of uncertain systems in the absence of matching assumptions_, Int. J. Contr., 45 (1987), pp. 1527-1542. 
- Z. Qu, _Robust control of nonlinear uncertain systems under generalized matching conditions_, Automatica, 29 (1993), pp. 985-998.  

A main concern with robust backstepping is the application of high gains, which causes high magnitude chattering in the control input. To overcome this, a flattened robust control Lyapunov function is introduced to reduce this chattering effect.















  