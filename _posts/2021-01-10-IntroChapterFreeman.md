---
layout: post
title: "(Book) _Robust Nonlinear Control Design_: Introduction, Part I"
author: "Kong Yao"
categories: posts
tags:
- robust control
- nonlinear control
image: post5.jpg
use_math: true
---
This note provides key ideas and takeaways from the introductory chapter of the book, "Robust Nonlinear Control Design", by R. Freeman and P. Kokotovic. For each idea/concept presented, explicit references (titles, authors etc.) are given immediately after they are cited in the book, to facilitate referencing and search in the future.

---

A common robust control paradigm is shown in Figure 1.1, consisting of a nominal plant $G$, a controller $K$ and an uncertainty $\Delta$. The objective in this robust control framework is to design $K$ such that it guarantees closed-loop stability and performance, for every $\Delta$ in a given family of uncertainties, $\mathcal F_{\Delta}$.  Therefore, selection of a suitable $\mathcal{F}_{\Delta}$ is critical in the robust control design.

![alt text](/assets/img/post5/rc_paradigm.PNG "Robust control paradigm")

In this framework, it is often assumed that $G$ is linear, finite-dimensional and time-invariant, and any form of nonlinearities can be encapsulated by choosing appropriate families, $\mathcal{F}_{\Delta}$. A large variety of these families have been considered and they include families of structured or unstructured uncertainties, time-invariant or time-varying uncertainties etc. The authors claim that this approach neglects the information on the nonlinearities and resulting control designs may be too conservative.

---

## Lyapunov Framework for Robust Control

Frequency domain methods are ubiquitous in robust linear control, but seldom seen in robust nonlinear control. State space methods are more common and have been more thoroughly developed for nonlinear systems.

One approach to determine stability of feedback connections of separate subsystems is to use nonlinear input-output methods, which are closely related to concepts in Lyapunov stability theory, detailed in these references:
### Nonlinear input-output methods
- I. W. Sandberg, _On the L2-boundedness of solutions of nonlinear functional equations_, Bell Sys. Tech. J., 43 (1964), pp. 1581-1599. 
- G. Zames, _On the input-output stability of time-varying nonlinear feedback systems. Part I: Conditions using concepts of loop gain, conicity, and positivity_, IEEE Trans. Automat. Contr., 11 (1966), pp. 228-238.
- G. Zames, _On the input-output stability of time-varying nonlinear feedback systems. Part II: Conditions involving circles in the frequency plane and sector nonlinearities_, IEEE Trans. Automat. Contr., 11 (1966), pp. 465-476. 
- C. A. Desoer and M. Vidyasagar, _Feedback Systems: Input-Output Properties_, Academic Press, New York, 1975. 
- M. Safonov, _Stability and Robustness of Multivariable Feedback Systems_, MIT Press, Cambridge, Massachusetts, 1980. 
- A. R. Teel, T. T. Georgiou, L. Praly, and E. D. Sontag, _Input-output stability, in The Control Handbook_, W. S. Levine, ed., CRC Press, 1996, pp. 895-908.

### Lyapunov stability theory
- A. M. Lyapunov, _Probleme general de la stabilite du mouvement, Ann. Fac. Sci. Toulouse, 9 (1907)_, pp. 203-474. In French
- T. Yoshizawa, _Stability Theory by Liapunov's Second Method_, The Mathematical Society of Japan, Gakujutsutosho Printing Co., Ltd., Tokyo, 1966.
- W. Hahn, _Stability of Motion_, Springer-Verlag, New York, 1967. 
- H. K. Khalil, _Nonlinear Systems_, Prentice Hall, Upper Saddle River, New Jersey, second ed., 1996.
- M. Vidyasagar, _Nonlinear Systems Analysis_, Prentice-Hall, Englewood Cliffs, New Jersey, second ed., 1993. 

### Dissipativity theory
An alternative formulation is to apply the theory of dissipativity, where a Lyapunov-like storage function is used to provide connections between input/output and state space stability. References of this approach can be found in:
- J. C. Willems, _Dissipative dynamical systems, Part I: General theory_, Arch. Rational Mech. Anal., 45 (1972), pp. 321-351.
- D. J. Hill and P. J. Moylan, _The stability of nonlinear dissipative systems_, IEEE Trans. Automat. Contr., 21 (1976), pp. 708-711. 
- D. J. Hill and P. J. Moylan, _Connections between finite-gain and asymptotic stability_, IEEE Trans. Automat. Contr., 25 (1980), pp. 931-936. 
- D. J. Hill, _Dissipative nonlinear systems: Basic properties and stability analysis_, in Proceedings of the 31st IEEE Conference on Decision and Control, Tucson, Arizona, Dec. 1992, pp. 3259-3264. 

---

There exist a number of robust nonlinear control frameworks and here are three that are relevant in this book. The first is the Lyapunov min-max approach, also known as "guaranteed stability", with the following references:
### Guaranteed stability
- G. Leitmann, _Guaranteed ultimate boundedness for a class of uncertain linear dynamical systems_, IEEE Trans. Automat. Contr., 23 (1978), pp. 1109-1110. 
- S. Gutman, _Uncertain dynamical systems--Lyapunov min-max approach_, IEEE Trans. Automat. Contr., 24 (1979), pp. 437-443. 
- G. Leitmann, _Guaranteed asymptotic stability for some linear systems with bounded uncertainties_, ASME J. Dynam. Syst. Meas. Contr., 101 (1979), pp. 212-216. 
- M. J. Corless and G. Leitmann, _Continuous state feedback guaranteeing uniform ultimate boundedness for uncertain dynamic systems_, IEEE Trans. Automat. Contr., 26 (1981), pp. 1139-1144.
- B. R. Barmish, M. J. Corless, and G. Leitmann, _A new class of stabilizing controllers for uncertain dynamical systems_, SIAM J. Contr. Optimiz., 21 (1983), pp. 246-255. 

### Nonlinear $H_{\infty}$ control
With the theory of dissipativity, the application of game theory led to nonlinear $H_{\infty}$ approach to robust nonlinear control, which can be found in:
- T. Basar and P. Bernhard, _Hinfinity-Optimal Control and Related Minimax Design Problems_, Birkh~user, Boston, second ed., 1995. 
- A. J. Van Der Schaft, _On a state space approach to nonlinear Hinfinity control_, Syst. Contr. Lett., 16 (1991), pp. 1-8. 
- A. J. Van Der Schaft, _L2-gain analysis of nonlinear systems and nonlinear state feedback Hinfinity control_, IEEE Trans. Automat. Contr., 37 (1992), pp. 770-784. 
- A. Isidori and A. Astolfi, _Disturbance attenuation and Hinfinity-control via measurement feedback in nonlinear systems_, IEEE Trans. Automat. Contr., 37 (1992), pp. 1283-1293. 
- J. A. Ball, J. W. Helton, and M. L. Walker, )Hinfinity control for nonlinear systems with output feedback_, IEEE Trans. Automat. Contr., 38 (1993), pp. 546-559. 
- A. J. Krener, _Necessary and sufficient conditions for nonlinear worst case (Hinfinity) control and estimation_, J. Math. Syst. Estim. Contr. To appear. 
- M. R. James and J. S. Baras, _Robust Hinfinity output feedback control for nonlinear systems_, IEEE Trans. Automat. Contr., 40 (1995), pp. 1007-1017.

### Input-to-state stability (ISS)
Finally, the concept of input-to-state stability (ISS) led to an input-output method related to Lyapunov stability,
- E. D. Sontag, _Further facts about input to state stabilization_, IEEE Trans. Automat. Contr., 35 (1990), pp. 473-476. 
- E. D. Sontag, _Input/output and state-space stability_, in New Trends in System Theory, Birkh~user, Boston, 1991. 
- I. M. Y. Mareels and D. J. Hill, _Monotone stability of nonlinear feedback systems_, J. Math. Syst. Estim. Contr., 2 (1992), pp. 275-291. 
- Y. Lin, E. D. Sontag, and Y. Wang, _Recent results on Lyapunov-theoretic techniques for nonlinear stability_, in Proceedings of the 1994 American Control Conference, Baltimore, Maryland, June 1994, pp. 1771-1775. 
- L. Praly and Z.-P. Jiang, _Stabilization by output feedback for systems with ISS inverse dynamics_, Syst. Contr. Lett., 21 (1993), pp. 19-33. 
- A. R. Teel and L. Praly, _On output feedback stabilization for systems with ISS inverse dynamics and uncertainties_, in Proceedings of the 32nd IEEE Conference on Decision and Control, San Antonio, Texas, Dec. 1993, pp. 1942-1947. 
- A. R. Teel, _A nonlinear small gain theorem for the analysis of control systems with saturation_, IEEE Trans. Automat. Contr., (1994). To appear. 
- Z.-P. Jiang, A. R. Teel, and L. Praly, _Small-gain theorem for ISS systems and applications_, Math. Control Signals Systems, 7 (1994), pp. 95-120. 
- E. D. Sontag, _State-space and I/O stability for nonlinear systems_, in Feedback Control, Nonlinear Systems, and Complexity, B. A. Francis and A. R. Tannenbaum, eds., Lecture Notes in Control and Information Sciences, Springer-Verlag, Berlin, 1995, pp. 215-235. 
- E. D. Sontag and Y. Wang, _On characterizations of the input-to-state stability property_, Syst. Contr. Lett., 24 (1995), pp. 351-359. 
- E. D. Sontag and Y. Wang, _New characterizations of input-to-state stability_, in Proceedings of the Conference on Information Sciences and Systems, Princeton, New Jersey, Mar. 1996. To appear. 
- Z.-P. Jiang, I. Mareels, and Y. Wang, _A Lyapunov formulation of nonlinear small gain theorem for interconnected systems_, in Proceedings of the IFAC Nonlinear Control Systems Design Symposium, Tahoe City, California, June 1995, pp. 666-671. 

---

In Chapter 3 of the book, a Lyapunov framework that combines the guaranteed stability and ISS frameworks is developed. In the problem formulation, set-valued maps are used to describe constraints. Usage of set-valued maps in control theory dates back to the early sixties and is currently used in viability theory for differential inclusions and nonsmooth analysis. Here are the references:
### Set-valued maps
- A. F. Filippov, _On certain questions in the theory of optimal control_, SIAM J. Control, 1 (1962), pp. 76-84. 
- T. Wazewski, _On an optimal control problem_, in Proceedings of the Conference on Differential Equations and Their Applications, Prague, 1963, pp. 229-242. 

### Viability Theory for differential inclusions
- J. S. Shamma, _Construction of nonlinear feedback for l1-optimal control_, in Proceedings of the 33rd IEEE Conference on Decision and Control, Lake Buena Vista, Florida, Dec. 1994, pp. 40-45.
- J. S. Shamma, _Optimization of the e~-induced norm under full state feedback_, IEEE Trans. Automat. Contr., 41 (1996). To appear. 
- J.-P. Aubin, _Viability Theory_, Birkhs Boston, 1991. 
- M. Kisielewicz, _Differential Inclusions and Optimal Control_, PWN-Polish Scientific Publishers, Warszawa, Poland, 1991.

### Nonsmooth analysis
- F. H. Clarke, _Qualitative properties of trajectories of control systems: A survey_, J. Dynam. Contr. Syst. To appear. 
- B. S. Mordukhovich, _Generalized differential calculus for nonsmooth and set-valued mappings_, Journal of Mathematical Analysis and Applications, 183 (1994), pp. 250-288. 
- B. S. Mordukhovich, _Necessary optimality and conhvllability conditions for nonsmooth control systems_, in Proceedings of the 33rd IEEE Conference on Decision and Control, Lake Buena Vista, Florida, Dec. 1994, pp. 3992-3997. 











  