---
layout: article
title: Digital Plasticine - Shader
tags: Shaders Physically_Based_Rendering BRDF_implementation Textures Godot GDShader
cover: /assets/plasticine_shader/PlasticinePlus_Text_general2.png
#article_header:
#  type: cover
#  image:
#    src: /assets/PlasticinePlus_Text_general.png
---

You can check out the project [here.](https://github.com/luisortpal/Digital-Plasticine) 

My Bachelor's thesis consisted on creating a digital representation of plasticine for Godot. This post will cover how the visual component of the material was replicated through the use of PBR models and textures. The article ["Plasticine Shading"](https://dl.acm.org/doi/10.1145/2668904.2668933) by Lindsey Howell, Philip Child and Peter Hall was the primary source for this section of the project.

<!--more-->

<h2>Plasticine Models</h2>
The article proposes two models: 

- The <b>"Plasticine model"</b> which, by modifying the BRDF, manages to get a more faithful representation of the material than what the state of the art models could achieve at the time.

- The <b>"Plasticine Plus model"</b> which obtains a better representation of the oiliness of the material and its shadows by expanding the G component of the plasticine model in exchange of a higher performance cost.

Both models were implemented, giving the artist the option to switch between them from the inspector.
<!--more-->

<center>
<h3>Plasticine model results</h3>
<div class="mt-3">
    <div class="mb-2">
        <img class="image image--xl" src="/assets/plasticine_shader/Plasticine_general.png">
        <img class="image image--xl" src="/assets/plasticine_shader/Plasticine_specular2.png">
    </div>
</div>
<i>The image on the left shows a general view. The one on the right shows the specular reflection obtained at grazing angles.</i>
</center>

<center>
<h3>Plasticine plus model results</h3>
<div class="mt-3">
    <div class="mb-2">
        <img class="image image--xl" src="/assets/plasticine_shader/PlasticinePlus_general.png">
        <img class="image image--xl" src="/assets/plasticine_shader/PlasticinePlus_specular.png">
    </div>
</div>
<i>The image on the left shows a general view. The one on the right shows the specular reflection obtained at grazing angles.</i>
</center>

<!--more-->

<h2>Textures</h2>
Plasticine is a highly plastic material which usually leads to surface imperfections and  marks after being manipulated. Textures have been used to recreate this effect in the following ways: 

- A <b>fingerprint texture</b> is applied to the material to recreate the marks that are left after handling. A <b>normal map</b> has also been used to replicate the light preassure that is applied when the plasticine is being held. Both textures were obtained from [TextureCan](https://www.texturecan.com/details/212/).

- For <b>surface imperfections</b>, a <b>noise map</b> of cellular type was created through the tool FastNoiseLite provided by Godot. That noise map was latter transformed into a normal map to achieve the desired effect.

<!--more-->

<h2>Final Result</h2>
<center>
<h3>Plasticine model</h3>
<div class="mt-3">
    <div class="mb-2">
        <img class="image image--xl" src="/assets/plasticine_shader/Plasticine_Text_general2.png">
        <img class="image image--xl" src="/assets/plasticine_shader/Plasticine_Text_specular2.png">
    </div>
</div>
<i>The image on the left shows a general view. The one on the right shows the specular reflection obtained at grazing angles.</i>
</center>

<center>
<h3>Plasticine plus model</h3>
<div class="mt-3">
    <div class="mb-2">
        <img class="image image--xl" src="/assets/plasticine_shader/PlasticinePlus_Text_general2.png">
        <img class="image image--xl" src="/assets/plasticine_shader/PlasticinePlus_Text_specular3.png">
    </div>
</div>
<i>The image on the left shows a general view. The one on the right shows the specular reflection obtained at grazing angles.</i>
</center>

<!--more-->

<h2>References</h2>

- The <b>refractive index</b> of the material was obtained from the article ["Terahertz detection of fingerprint spoofing"](https://www.researchgate.net/publication/349993911_Terahertz_detection_of_fingerprint_spoofing) by Norbert Pałka, Marcin Kowalski
- The article ["Plasticine Shading"](https://dl.acm.org/doi/10.1145/2668904.2668933) by Lindsey Howell, Philip Child and Peter Hall.
- Fingerprint textures were obtained from [TextureCan](https://www.texturecan.com/details/212/)

