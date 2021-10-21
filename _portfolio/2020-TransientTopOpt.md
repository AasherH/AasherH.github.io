---
title: "Transient Topology Optimization for Heat Conduction"
excerpt: "Programmed a transient topology optimization to minimize the global heat complicance under periodic thermal loading. <br/> <img src='/images/TransientThermalTopOpt.gif'>"
collection: portfolio
---

The support structures generated in additive manufacturing are subject to extreme thermal stresses and can deform during the part-printing process, ultimately yielding a failed part.
Thus, it is desirable to reduce the thermal stresses to improve part manufacturability.
This research aims to utilize topology optimization to minimize the global heat compliance in heat-conduction problems. 
A finite-element based topology optimization program is written, in Python, to solve this problem. Sensitivity analysis is solved via the adjoint-variable method, and geometry updating is accomplished via the Optimality Criteria.
Results are demonstrated on a two-dimensional rectangular domain with sinusoidal heat loading.
The purpose of this work was to develop my own skillset in topology optimization - all results are replicated based the mathematical development described in *Zhuang, C., & Xiong, Z. (2014). A global heat compliance measure based topology optimization for the transient heat conduction problem. Numerical Heat Transfer, Part B: Fundamentals, 65(5), 445-471.* 