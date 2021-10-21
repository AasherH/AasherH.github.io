---
title: "GPU-Accelerated Ray-Tracing for View Factors"
excerpt: "Developed a GPU-accelerated methodology to calculate the radition view factors of an arbitrary CAD file. This program was used to study thermoelectric generators (TEGs). <br/><img src='/images/TEG.JPG'>"
collection: portfolio
---

A robust computational framework was developed and implemented to numerically resolve the radiation view factor, , within three-dimensional geometries, and, in particular, thermoelectric generators (TEGs).
The proposed numerical methodology utilizes a graphics processing unit-accelerated ray-tracing algorithm to capitalize on the parallel nature of the view factor formulation.
The shadow effect, resulting from interference with the TEGs conductive interconnectors and thermoelectric legs, was accounted for via the Möller-Trumbore ray-triangle intersection algorithm with back-face culling enabled.
The effect of interconnector thickness, thermoelectric leg height-to-width ratios, TEG packing density, and the number of junctions on  is explored for various TEG configurations. Validation is performed against analytical values for planar and non-planar geometries, in addition to a point-in-polygon intersection algorithm for single-junction TEGs.
Results indicate that for a constant packing density,  asymptotically decreases with increasing distance across the TEG’s hot- and cold-sides.
For an increasing packing density and constant distance across the TEG’s junction,  decreases.
In a multi-junction device,  was found to asymptotically increase with junction number, implying that for large multi-junction TEG designs, a simpler model may serve to accurately predict the view factor.
The code developed herein is open-source and can be found at [GPU-Accelerated View Factor Calculator](https://github.com/AasherH/GPU-Accelerated-View-Factor-Calculator).