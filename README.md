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

You can modify these profiles by editing the source code. Please remember that they cannot be longer than the frequency tables inside the kernel you are patching. Also, 1.375v is currently the upper limit as it is capped elsewhere in most RK3188 kernels, perhaps this can also be patched in the binary but I don't know how yet.

Usage (RK3188):  
./overclockomatic kernel.img

Usage (RK3066):  
./overclockomatic3066 kernel.img

RK3066 USERS PLEASE READ!!!  
Overclocking your GPU might make your device slower if you do not also modify init.rc in your boot.img. For example, if you change the GPU profile from 266/400mhz to 266/533mhz and your init.rc reads the following:  
insmod /system/lib/modules/mali.ko mali_dvfs=50,100,133,160,200,266,400
Then the 533mhz might be ignored an you'll end up with 266mhz instead. Editing init.rc in boot.img can be rather difficult. I haven't tested this feature well yet. Please test both a "gpustock" version and an overclocked GPU version with antutu to confirm that the performance actually did increase.

The RK3066 version also tries to remove the CPU and GPU frequency limit. If this fails, it will only give a warning and continue. Please scroll your console up a bit to check for such warnings. The reason it fails can either be that there is no limit set in your kernel, or that the limit uses different frequencies than the ones this tool searches for. Please use Antutu before and after the modification to confirm that the performance actually did increase.

The RK3066 version also tries to patch the DDR init frequency, as many kernels might have DVFS disabled for the DDR RAM. Again, the patching might fail. You might not see much speed improvement on 720p, I didn't test 1080p yet.

Disclaimer
------
Use these tools at your own risk and only if you know what you're doing! Don't blame me if your stick burns to a crisp.
