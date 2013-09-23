RKPatchomatic
======
Rockchip Patchomatic Suite  
by phjanderson

More info / discussion:  
TODO

About
------
The Rockchip Patchomatic Suite allows you to modify RK3188 kernels without having to recompile them from source.

Vsyncfixomatic
------
Fixes frame skipping during video playback, a common issue on most RK3188 devices at this moment. It seems to be caused by vsync updating being disabled periodically during video playback. This tool tries to find that code and disable it.

Usage:  
./vsyncfixomatic kernel.img

Overclockomatic
------
Allows you to overclock your CPU/GPU/DDR. This tool will search for volt/frequency tables in the kernel and replaces them with new tables according to the "profiles" specified in the source code. One kernel file will be generated for each possible combination of CPU/GPU/DDR frequencies.

You can modify these profiles by editing the source code. Please remember that they cannot be longer than the frequency tables inside the kernel you are patching. Also, 1.375v is currently the upper limit as it is capped elsewhere in the kernel, perhaps this can also be patched in the binary but I don't know how yet.

Usage:  
./overclockomatic kernel.img

