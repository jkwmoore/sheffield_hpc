.. _torch_sharc:

Torch
=====

.. sidebar:: Torch

   :URL: http://torch.ch/

Torch is a scientific computing framework with wide support for machine learning algorithms that puts GPUs first. It is easy to use and efficient, thanks to an easy and fast scripting language, LuaJIT, and an underlying C/CUDA implementation.

About Torch on ShARC
--------------------

**A GPU-enabled worker node must be requested in order to use the GPU version of this software. See** :ref:`GPUComputing_sharc` **for more information.**

Torch is available on ShARC as both Singularity images and as a module.

This software and documentation is maintained by the `RSES group <http://rse.shef.ac.uk/>`_ and `GPUComputing@Sheffield <http://gpucomputing.shef.ac.uk/>`_. For feature requests or if you encounter any problems, please raise an issue on the `GPU Computing repository <https://github.com/RSE-Sheffield/GPUComputing/issues>`_.


Torch Singularity Images
------------------------

Singularity images are self-contained virtual machines similar to Docker. For more information on Singularity and how to use the images, see :ref:`singularity_sharc`.

A symlinked file is provided that always point to the latest image: ::

  /usr/local/packages/singularity/images/torch/gpu.img

To get a bash terminal in to an image for example, use the command: ::

  singularity exec /usr/local/packages/singularity/images/torch/gpu.img /bin/bash

The ``exec`` command can also be used to call any command/script inside the image e.g. ::

  singularity exec /usr/local/packages/singularity/images/torch/gpu.img th yourscript.lua

You may get a warning similar to ``groups: cannot find name for group ID ...``, this can be ignored and will not have an affect on running the image.

The paths ``/fastdata``, ``/data``, ``/home``, ``/scratch``, ``/shared`` are automatically mounted to your ShARC filestore directories. For GPU-enabled images the ``/nvlib`` and ``/nvbin`` is mounted to the correct Nvidia driver version for the node that you're using.

**To submit jobs that uses a Singularity image, see** :ref:`use_image_batch_singularity_sharc` **for more detail.**


Image Index
^^^^^^^^^^^

Paths to the actual images and definition files are provided below for downloading and building of custom images.

* Shortcut to Latest Image
    * ``/usr/local/packages/singularity/images/torch/gpu.img``
* GPU Images
    * Latest: v7-GPU-Ubuntu16.04-CUDA8-cudNN5.0 (GCC 5.4.0)
        * Path: ``/usr/local/packages/singularity/images/torch/v7-GPU-Ubuntu16.04-CUDA8-cudNN5.0.img``
        * Def file: :download:`/sharc/software/apps/singularity/torch_gpu.def </sharc/software/apps/singularity/torch_gpu.def>`

Using the Torch Module
----------------------

The following is an instruction on how to use the Torch module.

First request an interactive session, e.g. with :ref:`qrshx`. To use GPUs see :ref:`GPUInteractive_sharc`.

Load the Torch module which also loads anaconda 3.4, CUDA 8.0, cuDNN 5.1 and GCC 4.9.4. ::

	module load apps/torch/nvidia-7/gcc-4.9.4-cuda-8.0-cudnn-5.1-conda-3.4

On the DGX-1, load the NCCL library optimised for the hardware: ::

	moudle libs/nccl/dgx-1/binary-cuda-8.0

On any other node use a generic NCCL build: ::

	moudle load libs/nccl/generic/gcc-4.9.4-cuda-8.0


(Optional if you plan to interface with python) Create a conda environment to load relevant modules on your local user account and activate it ::

	conda create -n torch python=3.5
	source activate torch



Every Session Afterwards and in Your Job Scripts
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the interactive session or your batch script, load the relevant modules and (optionally) activate your conda environment ::

	module load apps/torch/nvidia-7/gcc-4.9.4-cuda-8.0-cudnn-5.1-conda-3.4

	#Optional
	source activate torch