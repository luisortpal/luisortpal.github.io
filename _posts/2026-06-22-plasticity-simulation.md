---
layout: article
title: Digital Plasticine - Plasticity simulation
tags: Simulation Voxel_Manipulation Marching_Cubes Optimization Godot GDScript
cover: /assets/plasticity_simulation/Voxel_sphere.png
#article_header:
#  type: cover
#  image:
#    src: /assets/PlasticinePlus_Text_general.png
---

You can check out the project [here.](https://github.com/luisortpal/Digital-Plasticine)

My Bachelor's thesis consisted on creating a digital representation of plasticine for Godot. This post will cover how the plasticity of the material was simulated. It's important to note that the objective wasn't to fully simulate the physics of the material due to how complex and time consuming it would be to develop. Instead, I aimed to simulate the sensation of playing with the material. 

<!--more-->

The article ["Interactive Global and Local Deformations for Virtual Clay"](https://ieeexplore.ieee.org/document/1238255) by Guillaume Dewaele and Marie-Paule Cani was the primary source for this section of the project. Because their proposal involves representing the object through a voxel grid, the [Marching Cubes](https://dl.acm.org/doi/10.1145/37402.37422) algorithm was implemented to translate it into a non-cubic 3D object so it can look closer to the material. 


<!--more-->

<h2>Grid Construction and Representation</h2>
The material is represented through a voxel grid with each cell having a mass density value. When the value is greater than cero the cell is drawn. An extra visualization mode was implemented to allow for easier debugging only rendering the faces of the cubes that the user is going to see to achieve a better performance. 

<center>
<div class="mt-3">
    <div class="mb-2">
        <img class="image image--xl" src="/assets/plasticity_simulation/Voxel_sphere.png">
    </div>
</div>
<i>The object made of cubes is the plasticine. The capsule is the player character that pushes the cells arround.</i>
</center>

<!--more-->

<h2>Plasticity Layers</h2>
The algorithm has three layers that interact with eachother to simulate the plasticity of the material.

- <b>Layer one</b> takes care of <b>large scale displacements</b> deciding which cells to move along side with the direction, distance and position of their final destination. If that position does not coincide with a viable grid cell, this layers distributes the mass density of the displaced cell proportionally between the neighbouring cells based on the  area it would occupy over each of them at the final position. 

<center>
<div class="mt-4">
    <div class="mb-2">
        <img class="image image--xl" src="/assets/plasticity_simulation/Voxel_sphere2.png">
        <img class="image image--xl" src="/assets/plasticity_simulation/Plasticidad_capa_1.png">
    </div>
</div>
<div class="mb-4">
    <i> On the left, the initial shape of a plasticine sphere with a radius of 3 cells. On the right, the displacement effects of layer one.</i>
</div>
</center>

- <b>Layer two</b> is in charge of <b>mass conservation</b>. Cells have a density cap. If they get overstuffed, this layer distributes the exceeding mass onto the neighbouring cells. If any of these gets overstuffed, it's treated by the layer the same way. Since this algorithm can be computationally expensive, it has been optimized to improve performance in many ways like, for example, limiting the number of iterations it's allowed to do each call.

<center>
<div class="mt-4">
    <div class="mb-2">
        <img class="image image--xl" src="/assets/plasticity_simulation/Plasticidad_capa_2.png">
    </div>
</div>
<div class="mb-4">
    <i> The displacement effects of layer two. The plasticine started as the same 3 cell radius sphere shown in layer one. The cubes at its corner have been slightly pushed.</i>
</div>
</center>

- <b>Layer three</b> simulates <b>surface tension</b>. When a new cell has a very low mass density, it must pass a series of checkmarks for it to be created. If it fails to do so,  its mass density is relocated to the nearest cell with available space. This is to avoid giving the illusion of increasing volume to the player.

<center>
<div class="mt-4">
    <div class="mb-2">
        <img class="image image--xl" src="/assets/plasticity_simulation/Plasticidad_capa_3_111.png">
        <img class="image image--xl" src="/assets/plasticity_simulation/Plasticidad_capa_3_1112.png">
    </div>
</div>
<div class="mb-4">
    <i>The effects of layer three. Shows how the cube closest to the top right corner disappears from one image to the next after being moved.</i>
</div>
</center>

<!--more-->

<h2>Marching Cubes</h2>
Marching Cubes is used to change the representation of the plasticine sphere into a non-cubic 3D object so it can look closer to the material. The algorithm travels through the grid cell by cell and, for each one, checks which vertices and how many of them are above or below the surface. Based on this, it selects one of 14 patterns to change what to draw inside the cell.       

<center>
<div class="mt-4">
    <div class="mb-2">
        <img class="image image--xl" src="/assets/plasticity_simulation/Voxel_sphere2.png">
        <img class="image image--xl" src="/assets/plasticity_simulation/MarchCube_sphere2.png">
    </div>
</div>
<div class="mb-4">
    <i> On the left, the initial shape of a plasticine sphere with a radius of 3 cells. On the right, the same sphere after applying Marching Cubes.</i>
</div>
</center>

<!--more-->

<h2>Final Result</h2>
<center>
    <div>
        {%- include extensions/youtube.html id='PZl-Z3E0Dr8' -%}
    </div>
</center>

<!--more-->

<h2>References</h2>

- The article ["Interactive Global and Local Deformations for Virtual Clay"](https://ieeexplore.ieee.org/document/1238255) by Guillaume Dewaele and Marie-Paule Cani
- The article ["Marching cubes: A high resolution 3D surface construction algorithm"](https://dl.acm.org/doi/10.1145/37402.37422) by William E. Lorensen and Harvey E. Cline.
- The video ["How to Create a Procedural Mesh using ArrayMesh in Godot - Optimized Voxels - Voxel Terrain #5"](https://www.youtube.com/watch?v=Pfqfr3zFyKI) was used as a guide for the  construction of the grid.
- Part of the code for the Marching Cubes section was taken from the ["Godot-Marching-Cubes"](https://github.com/SebLague/Godot-Marching-Cubes) github repository by SebLague 
