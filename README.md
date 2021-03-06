[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE.md)

dockerfiles
===========

Compilation of Dockerfiles with automated builds enabled on the [Docker Hub](https://hub.docker.com/u/kaixhin/). **Not suitable for production environments.** These images are under continuous development, so breaking changes may be introduced.

Nearly all images are based on Ubuntu Core 14.04 LTS, built with minimising size/layers and [best practices](https://docs.docker.com/articles/dockerfile_best-practices/) in mind. Dependencies are indicated left to right e.g. cuda-vnc is VNC built on top of CUDA. Explicit dependencies are excluded. CUDA images can be used without NVIDIA devices attached, but will obviously lack the ability to use CUDA capabilities.

Up-to-date builds
-----------------

Some builds based on certain software have builds that are triggered on schedule via a cron script to stay up to date on a weekly basis. These are:

- [Brainstorm](https://github.com/IDSIA/brainstorm)
- [Caffe](https://github.com/BVLC/caffe)
- [DIGITS](https://github.com/NVIDIA/DIGITS)
- [FGLab/FGMachine](https://kaixhin.github.io/FGLab)
- [Keras](https://github.com/fchollet/keras)
- [Lasagne](https://github.com/Lasagne/Lasagne)
- [MXNet](https://github.com/dmlc/mxnet)
- [neon](https://github.com/NervanaSystems/neon)
- [Pylearn2](https://github.com/lisa-lab/pylearn2)
- [Spearmint](https://github.com/HIPS/Spearmint)
- [Theano](https://github.com/Theano/Theano)
- [Torch](https://github.com/torch/distro)

Daemonising containers
----------------------

Most containers run as a foreground process. To daemonise such a container it is possible to use:

`docker run -d <image> sh -c "while true; do :; done"`

It is now possible to access the daemonised container, for example using bash:

`docker exec -it <id> bash`

Sibling containers
------------------

To start containers on the host from within a docker container, the following options should be used when running the container:

`-v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):$(which docker)`

The container also needs to have `lxc` installed.

CUDA
----

Many images rely on [CUDA](http://www.nvidia.com/object/cuda_home_new.html). All images that rely on CUDA have a CUDA 7.5 version, unless specified otherwise, with the "latest" tag on the Docker Hub (an additional "7.5" tag will be available once [issue #341](https://github.com/docker/hub-feedback/issues/341) is sorted). Some images also have CUDA 7.0 and 6.5 versions, with the "7.0" and "6.5" tags on the Docker Hub. The host must have the corresponding CUDA drivers (v352.39 for CUDA 7.5, v346.46 for CUDA 7.0, v340.29 for CUDA 6.5) installed for the kernel module. For a discussion of driver versions please see [issue #1](https://github.com/Kaixhin/dockerfiles/issues/1). The recommended way to get these driver versions is to use the `.run` installers.

The container must have all NVIDIA devices attached to it for CUDA to work properly. Therefore the command will be as such: `docker run -it --device /dev/nvidiactl --device /dev/nvidia-uvm --device /dev/nvidia0 kaixhin/cuda`. With 4 GPUs this would also have to include `--device /dev/nvidia1 --device /dev/nvidia2 --device /dev/nvidia3`.

NVIDIA now has an [experimental project](https://github.com/NVIDIA/nvidia-docker) which relies on a wrapper script to improve the usage of CUDA Docker containers. This is an alternative, but currently not a replacement, for this project. `kaixhin/cuda` will be deprecated once the official version is ready.

Helpers
-------

The scripts in this folder can provide extra functionality, e.g. SSH, to daemonised containers. Further details are available in the folder's readme.

Migration
---------

In the future it will hopefully be possible to checkpoint and restore Docker containers easily using [CRIU](http://criu.org/Docker). This would alleviate some issues, such as the inability to restart a VNC image successfully.

Automated Builds
----------------

[Automated Builds](https://docs.docker.com/docker-hub/builds/) on the Docker Hub have several advantages, including reproducibility and security. However the build cluster has the following limits for Automated Builds:

- 2 hours
- 1 CPU
- 2 GB RAM
- 512 MB swap
- 30 GB disk space

The main tip for keeping within the CPU and memory limits is to reduce parallelism/forking processes. Due to their logging system, redirecting stdout/stderr to /dev/null can potentially save a reasonable amount of memory.

Acknowledgements
----------------

Some Dockerfiles have been modified from the work of others. The source for these are:

- [CUDA](https://github.com/tleyden/docker)
- [Samba](https://github.com/dperson/samba)
- [VNC](https://github.com/dockerfile/ubuntu-desktop)

Citation
--------

If you find this useful in research please consider [citing this work](CITATION.md).
