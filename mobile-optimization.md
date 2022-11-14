# Mobile Optimization Guideline

## __Profiling__

* Try to profile both, in editor and in the target device.
* Save the profile results for a future comparison in performance.
* Profile early and often.
* Games runs better at 60 fps, but in mobile that would overhead the device, so go for at minimum 30fps.
* 30fps = 33.33 ms each frame, try to reach at MAX 65% maybe 70% of the frame time in processing so the device have time to cooldown, so at max use 22ms per frame.
* Try to identify if we are GPU-bound or CPU-bound:
    * if in the profiler __Gfx.WaitForCommands__ appears, the GPU is waiting for the CPU.
    * if __Gfx.WaitForPresent__ means the CPU is idle waiting for the GPU.
* Test on the “worst” or minimum device we want to develop for.
* When profiling take device temperature, the profiler might give bad performance reports because of it.

## __Memory__

* Use the new memory profiler, to know the memory footprint of your assets, it’s still on preview, but it’s stable enough.
* Reduce the impact of the garbage collection (the model used by unity stops the code execution, until finish, this might cause some stutter.
    * __strings__
        * Try to avoid the creation or manipulation of strings.
        * Avoid the frequent parsing of string-base objects like JSON and XML, prefer the use of __Protobuf__ or MessagePack.
        * Use the __StringBuilder__ class (C#) if we need to create a string at runtime.
    * __Unity Function Calls__
        * Calling for references of unity objects (like item.transform) generate a heap allocation, is better to create a reference when multiple calls are involved.
        * Use some functions that avoid garbage generation, for example __is better to use GameObject.CompareTag__ than comparing GameObject.tag with a string.
    * __Boxing__
        * Try to avoid passing objects as value, and instead use ref (references), passing a value generates a temporary item, and with that garbage.
    * __Coroutines__
        * Coroutines do not generate garbage on __yield__, but creating a new object like __WaitForSeconds__ does, it’s better to create a reference as a private variable, and use that one each time.
    * __LINQ and Regular Expressions__
        * Both generate some garbage in the behind-the-scenes, this improves with each C# iteration, but if we are having some issues with it, we can just simple avoid them.
* Manually Call Garbage Collection, if you are sure the gameplay is not going to be interrupted (like in a loading screen) __System.GC.Collect__
* Enable incremental GC.

## __Adaptive Performance__

Unity and Samsung developed toggether a Unity Package, that allows almost “automatically” a quality and performance adjustment,  based on different inputs, like desired framerate, device temperature, device bound by CPU or GPU and so on, it’s indispensable to be added to the project if mobile focused.

## __Programming and code architecture__

* Understand how the unity loop works, differences between __Awake, Start, Update__, and all of the other functions for the unity script lifecycle.
* Minimize the use of __Update, LateUpdate and FixedUpdate__
* if it’s needed to run some code constantly try to reduce the intervals for example:
```
    private int interval = 3; 
    void Update() 
    { 
        if (Time.frameCount % interval == 0) 
        {
            ExampleExpensiveFunction(); 
        } 
    } 
```
This would run the code only once every 3 frames instead of each one.
* Avoid doing super heavy load when in the functions __Awake, OnEnable, Start__, because this ones usually run BEFORE the application renders for the first time.
* Avoid empty functions specially if talking about Updates, they take resources to call.
* When getting/setting values from some unity objects, like Animator, Materials or Shaders, use their hash values instead of the property string (generate the reference at top and reuse in code)
* Use the minimum required data structure that the code requires to work, don’t use List or Dictionaries just because they are easy, follow the MSDN guide for data structures.
* Try to avoid adding components at runtime, spawning a prefab with all of the components is usually a lot more performant
* Avoid usage of functions like __GameObject.Find__, __GameObject.GetComponent__ in update functions, cache for a reference once in Start/Awake, and use the reference in update.
* Use objects pools, __Instantiate__ and __Destroy__ can generate spikes in performance and abused can generate a lot of garbage.
* Use __ScriptableObjects__ to store values that normally don’t change.

## __Project Configuration__

* If the Accelerometer is not used, disable the option in unity and if used, try to go for the lowest possible polling value.
* Disable __Auto Graphics API__ and select the target, this would reduce the amount of  shader variants generated.
* Disable __Target Architectures__ for older CPUs if we are not going to support them.
* Remove __Quality__ settings we are not going to need.
* If we don’t use physics remove __Auto Simulation__ and __Auto Sync Transforms__.
* Choose the right framerate, 30fps is good in mobile (if stable)
* Manually change FPS in slow or static scenes (like loading screens or menus)
* __AVOID LARGE HIERARCHIES.__
* Transform once, use __Transform.SetPositionAndRotation__ to apply both transformations in a single pass, also apply transform values, at instantiation.
* Vsync is always enable in mobile, so develop with it.

## Assets

* When Importing textures set the minimum value that produces an acceptable result.
* __Use textures in Power of Two (POT) ONLY!__
* Use __Texture Atlas__, this reduces draw calls, there are third party apps, super useful.
* Toggle off Read/Write Enabled option in textures.
* Disable unnecessary Mip Maps, like UI or 2D sprites.
* Compress textures in unity ATSC if targets recent Android and iOS, PVRTC for old iphones like iPhone 5, and ETC2 for Android devices prior 2016.
* Compress meshes inside unity, this compression only works in build size, but not memory footprint, don’t try to over “compress”, it can generate bad behaviours.
* Disable Read/Write in meshes.
* If the model does not require skeletal or blendshape animations disable them.
* Use as less as possible polygons for the models, use textures and normal maps for detailing.
* Use Addressable Asset System, so it can generate a smaller build and the end user can download the remaining assets from a CDN for example.

## __Graphics and GPU optimization__


* Batch your draw calls, Dynamic batching for grouping meshes with no more than 300 vertices, if the game doesn’t have any, disable it so no time is wasted in looking for them
* Static batching for non-moving geometry, it’s efficient but memory footprint is bigger.
* GPU instancing for larger groups of identical items (shared materials)
* SRP Batching, batching performed by the __Universal Render Pipeline__.
* Use the frame Debugger to find out what’s rendered each frame and troubleshoot shaders.
* __AVOID too many dynamic lights__, consider custom shader effects, light probes for dynamic meshes and baked lighting for static meshes.
* Disable shadows, either entirely, by mesh, and if possible fake shadows with blurred textures, in a mesh/quad under characters, or blob shadows with custom shaders.
* Bake lighting into lightmaps, meshes/lights need to be marked as __Contribute GI__, this lightmaps are fast and easy to show, use Progressive GPU Lightmapper to accelerate GI baking.
* Use Light Layers to confine objects in complex scenes, so light does not try to affect all the objects.
* Use light probes for moving objects.
* Use Level of Detail (__LOD__) 
* Use Occlusion Culling to remove hidden objects, mark your objects as Static Occluders or Occludees, and bake it in rendering.
* Don’t use native resolution of the device, use __Screen.SetResolution(width,height,false)__ to lower the output resolution and gain performance, this needs visual testing to find the limits.
* Limit the use of cameras to 1.
* Try to keep materials simple using __Unlit__ and __Lit__ from URP, specially the mobile ready ones.
* Try to avoid transparent or semi-transparent images, mobile devices are heavily impacted by it.
* Try to __avoid Post-processing effects__ specially fullscreen ones.
* In scripts try to avoid __Renderer.material__, this returns a reference to a new copy of the material.
* Use __SkinnedMeshRenderer__ only when needed.
* Minimize the use of __Reflection Probes__.

## __User Interface__

* Divide Canvases.
* Keep static elements in one canvas, and dynamic elements in other.
* Disable Invisible UI elements, this call the GPU draw calls.
* Limit __GraphicRaycasters__ and __Disable RaycastTarget, remove the canvas Graphic Raycaster__ and only add to the interactable elements like buttons, scrolls, and so on.
* Disable RaycastTarget on Text and Images.
* Try to avoid nesting of Layout groups, and don’t use the if the content isn’t dynamic.
* Avoid Large list and grid views, if you need one, try to use a pool of UI elements instead.
* UI elements that overlap (like cards in a deck) can create a lot of Draw calls, try to modify them in script (like actually only rendering 2)
* If using fullscreen UI, disable everything else, so we don’t use overhead, __NO TRANSPARENT FULLSCREEN MENUS__.
* Reduce application framerate in fullscreen menus.
* Prefer the usage of __Screen Space – Overlay.__

## __Audio__

* Use clips as mono, specially when using them in 3D spatial audio (if not force them in unity).
* Use uncompressed WAV files always.
* Compress the audio files inside unity.
    * Vorbis for most sounds or mp3 for no looping audios
    * ADPCM for short frequently use sounds like SFX.
* Small clips < 200 kb use Decompress on load.
* Medium clips >= 200kb use Compressed in memory.
* Large files (like music) set to streaming.

## __Animation__

* If the character does not need kinematics or animation retarget (like NPCs) use generic rig, otherwise, use humanoid rigs at minimum.
* Avoid abuse of Animators, for simple animations like changing values use a Tween tool, specially in UI environments.
* Use playables for simple animations or disable/dispose of animators, when finishing animations in no recurring animations.

## __Physics__

* Enable Prebake Collisions Meshes when possible (setting)
* Simplify Layer Collision Matrix
* Disable Auto Sync Transforms.
* Enable Reuse Collision Callbacks.
* SIMPLIFY COLLIDERS, BOX = BETTER!!
* Move rigidbodies using physics methods, avoid moving them with transforms and move physics elements on FixedUpdate instead of Update.
* Fix the Fixed timestep for physics, try to match the desired fps target, like 0.03 for 30fps
* Use the physics Debugger to troubleshoot problems with collisions or discrepancies.

## __Workflow Recommendations__

* Use version control, and set the editor to force serialization to Text.
* Use Unity’s Smart Merge for merging Scenes and Prefabs.
* Break Large Scenes in multiple small ones, load the scenes in Async additivie mode at runtime.
* __REMOVE UNUSED RESOURCES!! INCLUDING ASSETS BUNDLED WITH TOOLS, PURCHASES AND/OR PLUGINS__