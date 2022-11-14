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