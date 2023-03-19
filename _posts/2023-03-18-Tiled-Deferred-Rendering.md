---
layout: post
title: Tiled Deferred Rendering
subtitle: The Forge
categories: Graphics Project
tags: [C++, TheForge Engine, Vulkan, DirectX12, 3D, FSL]
thumbnail: "/assets/images/TiledDeferredScene.png"
---
 
## Tiled Deferred Rendering
- [Implemented with The Forge engine](https://github.com/ConfettiFX/The-Forge)
- Used PBR for multi-renderTarget in Deferred Rendering
- Light culling using tile frustums in a compute shader
- Depth Bound pass([Parallel reduction](https://diaryofagraphicsprogrammer.blogspot.com/2014/03/compute-shader-optimizations-for-amd.html))
- Employed a seperate buffer for light position and color values for better performance.


<div style="text-align: center">
	<img src="/assets/images/TiledDeferredScene.png"
	 	width="1280"
	 	height="720"
     	alt="4096 Light scene">
</div>
<p style="text-align: center;">
4096 Lights Render Scene
</p>

To debug scene, I used a [logarithmic scale](https://en.wikipedia.org/wiki/Logarithmic_scale) to divide color section. 

<div style="text-align: center">
	<img src="/assets/images/TiledDeferredDebug.png"
	 	width="1280"
	 	height="720"
     	alt="4096 Light Debug Scene">
</div>
<p style="text-align: center;">
4096 Lights Debug Scene
</p>

<br>
<br>

<iframe width="420" height="315" src="https://www.youtube.com/embed/OpTEyCmxMXs" frameborder="0" allowfullscreen></iframe>


