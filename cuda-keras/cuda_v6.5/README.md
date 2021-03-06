[![Docker Pulls](https://img.shields.io/docker/pulls/kaixhin/cuda-keras.svg)](https://hub.docker.com/r/kaixhin/cuda-keras/)
[![Docker Stars](https://img.shields.io/docker/stars/kaixhin/cuda-keras.svg)](https://hub.docker.com/r/kaixhin/cuda-keras/)

cuda-keras
==========
Ubuntu Core 14.04 + [CUDA 6.5.14](http://www.nvidia.com/object/cuda_home_new.html) + [Keras](http://keras.io/).

Requirements
------------

- Host with corresponding CUDA drivers (v. 340.29) installed for the kernel module.

Usage
-----
The container must have all NVIDIA devices attached to it for CUDA to work properly.
Therefore the command will be as such: `docker run -it --device /dev/nvidiactl --device /dev/nvidia-uvm --device /dev/nvidia0 kaixhin/cuda-keras`.
With 4 GPUs this would also have to include `--device /dev/nvidia1 --device /dev/nvidia2 --device /dev/nvidia3`.

For more information on CUDA on Docker, see the [repo readme](https://github.com/Kaixhin/dockerfiles#cuda).

Citation
--------
If you find this useful in research please consider [citing this work](https://github.com/Kaixhin/dockerfiles/blob/master/CITATION.md).
