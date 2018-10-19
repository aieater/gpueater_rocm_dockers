
## Docker

#### Available images

https://hub.docker.com/r/gpueater/ubuntu16-rocm-1.9.211-tensorflow-1.11.0/

https://hub.docker.com/r/gpueater/rocm-tensorflow-1.8/

### Latest

```
docker run -it --device=/dev/kfd --device=/dev/dri gpueater/ubuntu16-rocm-1.9.211-tensorflow-1.11.0
```

### Old images

```
docker run -it --device=/dev/kfd --device=/dev/dri gpueater/rocm-tensorflow-1.8
```

<br>
<br>
<br>

## ROCm1.9.211+TensorFlow 1.11.0 image for AMD Radeon GPU




###  # Recommended environment of host

 OS: Ubuntu16.04.05+
 Kernel: 4.15+
 ROCm: 1.9.211+

### # AMD Radeon driver installation on Host

#### - Update linux kernel

 \* If you already used the GPUEater AMD GPU instance, the following command is not required.

```sh
sudo apt update
sudo apt upgrade -y
sudo apt install -y linux-generic-hwe-16.04
sudo reboot
```

#### - Install AMD GPU Driver (ROCm)

 \* If you already used the GPUEater AMD GPU instance, the following command is not required.

```sh
sudo apt install -y wget
wget -qO - http://repo.radeon.com/rocm/apt/debian/rocm.gpg.key | sudo apt-key add -
sudo sh -c 'echo deb [arch=amd64] http://repo.radeon.com/rocm/apt/debian/ xenial main > /etc/apt/sources.list.d/rocm.list'
sudo apt install -y libnuma-dev rocm-dkms
sudo usermod -a -G video $LOGNAME
```

#### - Make sure to see AMD Radeon GPUs.

```/opt/rocm/opencl/bin/x86_64/clinfo

ls -la /dev/kfd # AMD Kernel Fusion Driver
ls -la /dev/dri/ # Display and OpenCL file descriptors
```


###  # Docker-CE on Host

####  - Install docker-ce

https://docs.docker.com/install/linux/docker-ce/ubuntu/

####  - Run a container with GPU driver file descriptor.

```docker run -it --device=/dev/kfd --device=/dev/dri gpueater/ubuntu16-rocm-1.9.211-tensorflow-1.11.0```



####  - Make sure GPUs in launched container

```sh
/opt/rocm/opencl/bin/x86_64/clinfo

Number of platforms:				 1
  Platform Profile:				 FULL_PROFILE
  Platform Version:				 OpenCL 2.1 AMD-APP.internal (2574.0)
  Platform Name:				 AMD Accelerated Parallel Processing
  Platform Vendor:				 Advanced Micro Devices, Inc.
  Platform Extensions:				 cl_khr_icd cl_amd_object_metadata cl_amd_event_callback 


  Platform Name:				 AMD Accelerated Parallel Processing
Number of devices:				 1
  Device Type:					 CL_DEVICE_TYPE_GPU
  Vendor ID:					 1002h
  Board name:					 Device 687f
  Device Topology:				 PCI[ B#3, D#0, F#0 ]
  Max compute units:				 56
  Max work items dimensions:			 3
    Max work items[0]:				 1024
    Max work items[1]:				 1024
    Max work items[2]:				 1024
  Max work group size:				 256
  Preferred vector width char:			 4
  Preferred vector width short:			 2
  Preferred vector width int:			 1
  Preferred vector width long:			 1
  Preferred vector width float:			 1
  Preferred vector width double:		 1
  Native vector width char:			 4
  Native vector width short:			 2
  Native vector width int:			 1
  Native vector width long:			 1
  Native vector width float:			 1
  Native vector width double:			 1
  Max clock frequency:				 1622Mhz
  Address bits:					 64
  Max memory allocation:			 7287183769
  Image support:				 Yes
  Max number of images read arguments:		 128
  Max number of images write arguments:		 8
  Max image 2D width:				 16384
  Max image 2D height:				 16384
  Max image 3D width:				 2048
  Max image 3D height:				 2048
  Max image 3D depth:				 2048
  Max samplers within kernel:			 26751
  Max size of kernel argument:			 1024
  Alignment (bits) of base address:		 1024
  Minimum alignment (bytes) for any datatype:	 128
  Single precision floating point capability
    Denorms:					 Yes
    Quiet NaNs:					 Yes
    Round to nearest even:			 Yes
    Round to zero:				 Yes
    Round to +ve and infinity:			 Yes
    IEEE754-2008 fused multiply-add:		 Yes
  Cache type:					 Read/Write
  Cache line size:				 64
  Cache size:					 16384
  Global memory size:				 8573157376
  Constant buffer size:				 7287183769
  Max number of constant args:			 8
  Local memory type:				 Scratchpad
  Local memory size:				 65536
  Max pipe arguments:				 16
  Max pipe active reservations:			 16
  Max pipe packet size:				 2992216473
  Max global variable size:			 7287183769
  Max global variable preferred total size:	 8573157376
  Max read/write image args:			 64
  Max on device events:				 0
  Queue on device max size:			 0
  Max on device queues:				 0
  Queue on device preferred size:		 0
  SVM capabilities:				 
    Coarse grain buffer:			 Yes
    Fine grain buffer:				 Yes
    Fine grain system:				 No
    Atomics:					 No
  Preferred platform atomic alignment:		 0
  Preferred global atomic alignment:		 0
  Preferred local atomic alignment:		 0
  Kernel Preferred work group size multiple:	 64
  Error correction support:			 0
  Unified memory for Host and Device:		 0
  Profiling timer resolution:			 1
  Device endianess:				 Little
  Available:					 Yes
  Compiler available:				 Yes
  Execution capabilities:				 
    Execute OpenCL kernels:			 Yes
    Execute native function:			 No
  Queue on Host properties:				 
    Out-of-Order:				 No
    Profiling :					 Yes
  Queue on Device properties:				 
    Out-of-Order:				 No
    Profiling :					 No
  Platform ID:					 0x7f248a35f270
  Name:						 gfx900
  Vendor:					 Advanced Micro Devices, Inc.
  Device OpenCL C version:			 OpenCL C 2.0 
  Driver version:				 2574.0 (HSA1.1,LC)
  Profile:					 FULL_PROFILE
  Version:					 OpenCL 1.2 
  Extensions:					 cl_khr_fp64 cl_khr_global_int32_base_atomics cl_khr_global_int32_extended_atomics cl_khr_local_int32_base_atomics cl_khr_local_int32_extended_atomics cl_khr_int64_base_atomics cl_khr_int64_extended_atomics cl_khr_3d_image_writes cl_khr_byte_addressable_store cl_khr_fp16 cl_khr_gl_sharing cl_amd_device_attribute_query cl_amd_media_ops cl_amd_media_ops2 cl_khr_subgroups cl_khr_depth_images cl_amd_copy_buffer_p2p cl_amd_assembly_program 
```


Also see https://www.gpueater.com/help

Also see https://github.com/aieater/rocm_tensorflow_info
