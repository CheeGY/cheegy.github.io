---
layout: post
title: "Introductory Chapter from \"Robust Nonlinear Control Design\""
author: "Kong Yao"
categories: posts
tags: [robust control]
image: post5.jpg
use_math: true
---
This note provides key ideas and takeaways from the introductory chapter of the book, "Robust Nonlinear Control Design", by R. Freeman and P. Kokotovic. The other purpose of this note is to provide explicit references (titles, authors etc.) immediately after they are cited, in order to facilitate future reference.

---

A popular robust control paradigm is shown in Figure 1.1, consisting of a nominal plant $G$, a controller $K$ and an uncertainty $\Delta$. The objective in this robust control framework is to design $K$ such that it guarantees closed-loop stability and performance, for every $\Delta$ in a given family of uncertainties, $\mathcal F_{\Delta}$.  Therefore, selection of a suitable $\mathcal{F}_{\Delta}$ is critical in the robust control design.

![alt text](/assets/img/post5/rc_paradigm.PNG "Robust control paradigm")

In this framework, it is often assumed that $G$ is linear, finite-dimensional and time-invariant, and any form of nonlinearities can be encapsulated by choosing appropriate families, $\mathcal{F}_{\Delta}$. A large variety of these families have been considered and they include families of structured or unstructured uncertainties, time-invariant or time-varying uncertainties etc. The authors claim that this approach neglects the information on the nonlinearities and resulting control designs may be too conservative.

---

## Lyapunov Framework for Robust Control

Frequency domain methods are ubiquitous in robust linear control, but seldom seen in robust nonlinear control. State space methods are more common and have been more thoroughly developed for nonlinear systems.

One approach to determine stability of feedback connections of separate subsystems is to use nonlinear input-output methods, which are closely related to concepts in Lyapunov stability theory, detailed in these references:

- A. M. Lyapunov, _Probleme general de la stabilite du mouvement, Ann. Fac. Sci. Toulouse, 9 (1907)_, pp. 203-474. In French
- T. Yoshizawa, _Stability Theory by Liapunov's Second Method_, The Mathematical Society of Japan, Gakujutsutosho Printing Co., Ltd., Tokyo, 1966.
- W. Hahn, _Stability of Motion_, Springer-Verlag, New York, 1967. 
- H. K. Khalil, _Nonlinear Systems_, Prentice Hall, Upper Saddle River, New Jersey, second ed., 1996.
- M. Vidyasagar, _Nonlinear Systems Analysis_, Prentice-Hall, Englewood Cliffs, New Jersey, second ed., 1993. 

Nonlinear input-output methods are described in:
- I. W. Sandberg, _On the L2-boundedness of solutions of nonlinear functional equations, Bell Sys. Tech. J., 43 (1964), pp. 1581-1599. 
- G. Zames, _On the input-output stability of time-varying nonlinear feedback systems. Part I: Conditions using concepts of loop gain, conicity, and positivity_, IEEE Trans. Automat. Contr., 11 (1966), pp. 228-238.
- G. Zames, _On the input-output stability of time-varying nonlinear feedback systems. Part II: Conditions involving circles in the frequency plane and sector nonlinearities_, IEEE Trans. Automat. Contr., 11 (1966), pp. 465-476. 
- C. A. Desoer and M. Vidyasagar, _Feedback Systems: Input-Output Properties_, Academic Press, New York, 1975. 
- M. Safonov, _Stability and Robustness of Multivariable Feedback Systems_, MIT Press, Cambridge, Massachusetts, 1980. 
- A. R. Teel, T. T. Georgiou, L. Praly, and E. D. Sontag, _Input-output stability, in The Control Handbook_, W. S. Levine, ed., CRC Press, 1996, pp. 895-908.

An alternative formulation is to apply the theory of dissipativity, where a Lyapunov-like storage function is used to provide connections between input/output and state space stability. References of this approach can be found in:
- J. C. Willems, _Dissipative dynamical systems, Part I: General theory_, Arch. Rational Mech. Anal., 45 (1972), pp. 321-351.
- D. J. Hill and P. J. Moylan, _The stability of nonlinear dissipative systems_, IEEE Trans. Automat. Contr., 21 (1976), pp. 708-711. 
- D. J. Hill and P. J. Moylan, _Connections between finite-gain and asymptotic stability_, IEEE Trans. Automat. Contr., 25 (1980), pp. 931-936. 
- D. J. Hill, _Dissipative nonlinear systems: Basic properties and stability analysis_, in Proceedings of the 31st IEEE Conference on Decision and Control, Tucson, Arizona, Dec. 1992, pp. 3259-3264. 



  