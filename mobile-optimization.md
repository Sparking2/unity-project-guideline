# Mobile Optimization Guideline

## Profiling

* Try to profile both, in editor and in the target device.
* Save the profile results for a future comparison in performance.
* Profile early and often.
* Games runs better at 60 fps, but in mobile that would overhead the device, so go for at minimum 30fps.
* 30fps = 33.33 ms each frame, try to reach at MAX 65% maybe 70% of the frame time in processing so the device have time to cooldown, so at max use 22ms per frame.
* Try to identify if we are GPU-bound or CPU-bound:
    * if in the profiler Gfx.WaitForCommands appears, the GPU is waiting for the CPU.
    * if Gfx.WaitForPresent means the CPU is idle waiting for the GPU.
* Test on the “worst” or minimum device we want to develop for.
* When profiling take device temperature, the profiler might give bad performance reports because of it.
