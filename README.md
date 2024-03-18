# Instant Neural Graphics Primitives for curriculum designing
![fox](https://github.com/souvikroy/Instant-Neural-Graphics-Primitives-for-Ed-tech/assets/4746631/97bf4eba-a025-4c99-9073-1b074edd0683)

![robot5](https://github.com/souvikroy/Instant-Neural-Graphics-Primitives-for-Ed-tech/assets/4746631/68c596d0-2a96-4c3f-b2a0-f515a11a86f5)


Ever wanted to train a NeRF model of a fox in under 5 seconds? Or fly around a scene captured from photos of a factory robot? Of course you have!

Here you will find an implementation of four neural graphics primitives, being neural radiance fields (NeRF), signed distance functions (SDFs), neural images, and neural volumes. In each case, we train and render a MLP with multiresolution hash input encoding using the tiny-cuda-nn framework.


# Installation

If you have Windows, download one of the following releases corresponding to your graphics card and extract it. Then, start instant-ngp.exe.

RTX 3000 & 4000 series, RTX A4000–A6000, and other Ampere & Ada cards
RTX 2000 series, Titan RTX, Quadro RTX 4000–8000, and other Turing cards
GTX 1000 series, Titan Xp, Quadro P1000–P6000, and other Pascal cards
Keep reading for a guided tour of the application or, if you are interested in creating your own NeRF, watch the video tutorial or read the written instructions.

If you use Linux, or want the developer Python bindings, or if your GPU is not listed above (e.g. Hopper, Volta, or Maxwell generations), you need to build instant-ngp yourself.

# Usage
![testbed](https://github.com/souvikroy/Instant-Neural-Graphics-Primitives-for-Ed-tech/assets/4746631/b92b4940-3f11-4fb8-8d32-ede2981077be)

instant-ngp comes with an interactive GUI that includes many features:

* comprehensive controls for interactively exploring neural graphics primitives,
* VR mode for viewing neural graphics primitives through a virtual-reality headset,
* saving and loading "snapshots" so you can share your graphics primitives on the internet,
* a camera path editor to create videos,
* NeRF->Mesh and SDF->Mesh conversion,
* camera pose and lens optimization, and many more.

# NeRF fox

Simply start instant-ngp and drag the data/nerf/fox folder into the window. Or, alternatively, use the command line:

instant-ngp$ ./instant-ngp data/nerf/fox

![image](https://github.com/souvikroy/Instant-Neural-Graphics-Primitives-for-Ed-tech/assets/4746631/dbd4d8c6-02a2-42b5-ab8a-888e27adf3ef)


You can use any NeRF-compatible dataset, e.g. from original NeRF, the SILVR dataset, or the DroneDeploy dataset. To create your own NeRF, watch the video tutorial or read the written instructions.

# SDF armadillo

Drag data/sdf/armadillo.obj into the window or use the command:

instant-ngp$ ./instant-ngp data/sdf/armadillo.obj

![image](https://github.com/souvikroy/Instant-Neural-Graphics-Primitives-for-Ed-tech/assets/4746631/d02b4ba5-4d04-4e89-b956-c52af81313d2)


To reproduce the gigapixel results, download, for example, the Tokyo image and convert it to .bin using the scripts/convert_image.py script. This custom format improves compatibility and loading speed when resolution is high. Now you can run:

instant-ngp$ ./instant-ngp data/image/tokyo.bin

# Volume renderer
Download the nanovdb volume for the Disney cloud, which is derived from here (CC BY-SA 3.0). Then drag wdas_cloud_quarter.nvdb into the window or use the command:

instant-ngp$ ./instant-ngp wdas_cloud_quarter.nvdb
![image](https://github.com/souvikroy/Instant-Neural-Graphics-Primitives-for-Ed-tech/assets/4746631/72f90384-4ad4-436b-ad42-758b2a335233)


# Building instant-ngp (Windows & Linux)
Requirements

* An NVIDIA GPU; tensor cores increase performance when available. All shown results come from an RTX 3090.
* A C++14 capable compiler. The following choices are recommended and have been tested:
* Windows: Visual Studio 2019 or 2022
Linux: GCC/G++ 8 or higher
* A recent version of CUDA. The following choices are recommended and have been tested:
Windows: CUDA 11.5 or higher
Linux: CUDA 10.2 or higher
* CMake v3.21 or higher.
* (optional) Python 3.7 or higher for interactive bindings. Also, run pip install -r requirements.txt.
* (optional) OptiX 7.6 or higher for faster mesh SDF training.
* (optional) Vulkan SDK for DLSS support.
* If you are using Debian based Linux distribution, install the following packages


# Compilation
Begin by cloning this repository and all its submodules using the following command:

$ git clone --recursive
$ cd instant-ngp
Then, use CMake to build the project: (on Windows, this must be in a developer command prompt)

instant-ngp$ cmake . -B build -DCMAKE_BUILD_TYPE=RelWithDebInfo
instant-ngp$ cmake --build build --config RelWithDebInfo -j
If compilation fails inexplicably or takes longer than an hour, you might be running out of memory. Try running the above command without -j in that case. If this does not help, please consult this list of possible fixes before opening an issue.

If the build succeeds, you can now run the code via the ./instant-ngp executable or the scripts/run.py script described below.

If automatic GPU architecture detection fails, (as can happen if you have multiple GPUs installed), set the TCNN_CUDA_ARCHITECTURES environment variable for the GPU you would like to use. The following table lists the values for common GPUs. If your GPU is not listed, consult this exhaustive list.

H100	40X0	30X0	A100	20X0	TITAN V / V100	10X0 / TITAN Xp	9X0	K80
90	89	86	80	75	70	61	52	37
