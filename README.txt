_--------------------------------------------------------------------------------
--------------------------------------------------------------------------------
CUDA by Example: An Introduction to General-Purpose GPU Programming
README.txt
--------------------------------------------------------------------------------
--------------------------------------------------------------------------------
July 2010
Copyright (C) 2010 NVIDIA Corp.



Distribution Contents
----------------------------------------------------
The end user license (license.txt)
Code examples from chapters 3-11 of 
     "CUDA by Example: An Introduction to General-Purpose GPU Programming"
Common code shared across examples
This README file (README.txt)



Compiling the Examples
----------------------------------------------------
The vast majority of these code examples can be compiled quite easily by using 
NVIDIA's CUDA compiler driver, nvcc. To compile a typical example, say 
"example.cu," you will simply need to execute:

> nvcc example.cu

The compilation will produce an executable, a.exe on Windows and a.out on Linux.
To have nvcc produce an output executable with a different name, use the 
-o <output-name> option. To learn about additional nvcc options, run

> nvcc --help



Compiling Examples for Compute Capabilities > 1.0
----------------------------------------------------
The examples from Chapter 9, hist_gpu_gmem_atomics.cu and 
hist_gpu_shmem_atomics.cu, both require GPUs with compute capabilities greater 
than 1.0. Likewise, the examples from Appendix A, dot.cu and hashtable_gpu.cu,
also require a GPU with compute capability greater than 1.0.

Accordingly, these examples also require an additional argument in order to 
compile and run correctly. Since hist_gpu_gmem_atomics.cu requires compute 
capability 1.1 to function properly, the easiest way to compile this example
is,

> nvcc -arch=sm_11 hist_gpu_gmem_atomics.cu


Similarly, hist_gpu_shmem_atomics.cu relies on features of compute capability
1.2, so it can be compiled as follows:

> nvcc -arch=sm_12 hist_gpu_shmem_atomics.cu




Compiling Examples with OpenGL and GLUT Dependencies
----------------------------------------------------

The following examples use OpenGL and GLUT (GL Utility Toolkit) in order to 
display their results:

Chapter 4                       Chapter 7
    julia_cpu.cu                    heat.cu 
    julia_gpu.cu                    heat_2d.cu

Chapter 5                       Chapter 8
    ripple.cu                       basic.cu
    shared_bitmap.cu                basic2.cu
                                    heat.cu
Chapter 6                           ripple.cu
    ray.cu
    ray_noconst.cu


To build with OpenGL and GLUT, some additions will need to be made to the nvcc
command-line. These instructions are different on Linux and Windows operating 
systems.


Linux
-----------------------
On Linux, you will first need to ensure that you have a version of GLUT 
installed. One method for determining whether GLUT is correctly installed is 
simply attempting to build an example that relies on GLUT. To do this, one
needs to add -lglut to the nvcc line, indicating that the example needs to be
linked against libglut. For example:

> nvcc -lglut julia_gpu.cu

If you get an error about missing GL/glut.h or a link error similar to the 
following, GLUT is not properly installed:

    /usr/bin/ld: cannot find -lglut


If you need to install GLUT, we recommend using freeglut on Linux systems. As
always with Linux, there exist a variety of ways to install this package, 
including downloading and building a source package from
http://freeglut.sourceforge.net/

The easiest method involves exploiting the package managers available with many
Linux distributions. Two common methods are given here:

> yum install freeglut-devel

> apt-get install freeglut-dev


