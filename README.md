RKPatchomatic
======
Rockchip Patchomatic Suite  
by phjanderson

More info / discussion:  
[Freaktab](http://www.freaktab.com/showthread.php?7150-rkpatchomatic-tool-overclock-vsync-fix-any-binary-rk3188-kernel!)

About
------
The Rockchip Patchomatic Suite allows you to modify RK3188 and RK3066 kernels without having to recompile them from source.

Vsyncfixomatic (RK3188 only!)
------
Fixes frame skipping during video playback, a common issue on most RK3188 devices at this moment. It seems to be caused by vsync updating being disabled periodically during video playback. This tool tries to find that code and disable it.

Usage:  
./vsyncfixomatic kernel.img

Overclockomatic
------
Allows you to overclock your CPU/GPU/DDR. This tool will search for volt/frequency tables in the kernel and replaces them with new tables according to the "profiles" specified in the source code. One kernel file will be generated for each possible combination of CPU/GPU/DDR frequencies.

You can modify these profiles by editing the source code. Please remember that they cannot be longer than the frequency tables inside the kernel you are patching.

Usage (RK3188):  
./overclockomatic3188 kernel.img

Usage (RK3066):  
./overclockomatic3066 kernel.img

RK3066 USERS PLEASE READ!!!  
The GPU overclock doesn't seem to work for 3066 devices. You could try the 400mhz if your device is currently clocked to 266mhz, but please test both the "gpustock" and overclocked GPU version with antutu to confirm that the performance actually did increase, it might decrease even!

The RK3066 version also tries to remove the CPU and GPU frequency limit. If this fails, it will only give a warning and continue. Please scroll your console up a bit to check for such warnings. The reason it fails can either be that there is no limit set in your kernel, or that the limit uses different frequencies than the ones this tool searches for. Please use Antutu before and after the modification to confirm that the performance actually did increase.

The RK3066 version also tries to patch the DDR init frequency, as many kernels might have DVFS disabled for the DDR RAM. Again, the patching might fail. You might not see much speed improvement on 720p, I didn't test 1080p yet.

Disclaimer
------
Use these tools at your own risk and only if you know what you're doing! Don't blame me if your stick burns to a crisp.
