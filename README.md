# Latentfusion

Fork of Dr. Keunhong Park's LatentFusion. Off all of the systems we have looked at, this seems to be most promising as we don't need to train the main network, only figure out how to create the "latent" representation of the object. Essentially learn to add new objects to MOPED dataset. This markdown's main purpose is to keep record to key steps and procedures. Some theoritical study is in my "6D_OBJECT_POSE_ESTIMATION" notes

* Fork: https://github.com/Mechazo11/latentfusion-az-fork

* [Code](https://github.com/Omni6DPose/Omni6DPoseAPI)

* [paper](https://arxiv.org/pdf/2406.04316)

* [video2](https://www.youtube.com/watch?v=tlzcq1KYXd8): This one goes in much in depth details

* [video1](https://www.youtube.com/watch?v=T6qSMYmlCj4): This one mainly shows results

* [project_website](https://latentfusion.github.io/)

# Testing LatentFusion with available data

![alt text](figs/: https://www.youtube.com/watch?v=ltxN3PITD0w.png)


## Setup:

* Install miniforge as shown here: https://github.com/conda-forge/miniforge

* Create the ```latentfusion``` environment: ```environment_updated.yml``` file: ```mamba env create -n latentfusion -f environment_updated.yml```

* Activate env using the shell script: ```source env.sh```. It ensures this directory is added to the ```$PYTHONPATH``` variable.

* First ensure Nvidia driver is installed and nvcc is configured to find the appropriate cuda driver

* Install pytorch with cuda support. This installs on system level: ```pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124```

* Test to make sure CUDA is found

```bash
python3
import torch
torch.cuda.is_available()
```


* Per-view object-to-space feature volume (or 3D latent voxel) is first generated. Then using Convolution Gated Recurrent UNit (ConvGRU), all the views are combined into one canonical representation. Hence the need for known pose and reference image view.
  
* Input image size needs to be 640 x 480
* How object pose estimation works? Given an image $\mathcal{I}$ and depth map $\mathcal{D}$ that provides a rotation $\mathcal{R}$ and a translation vector $t$. This together defines **object-to-camera** coordiante transformation $\mathcal{E} = [\mathcal{R}|t]$. Notice this is a 3 x 4 matrix similar to projection matrix $\mathbf{P}$.

* Rotations are parameterized in log-quaternion form $\mathbf{\omega} =  \{0, \omega_{1}, \omega_{2}, \omega_{3} \}$~

* To infer pose here are the following information required
* RGB image $\mathcal{I}$ and matched depth map $\mathcal{D}$
* Object segmentation mask $\mathcal{M}$
* 2D Bounding box (in pixel coordinate system)
* 2D segmentation (in pixel coordinate system)
* Coarse estimation: Predict translation as centroid of a bounding cube and then sample rotaiton using fibonacci lattice and then sample a random yaw angle.

# MODEL FREE POSE ESTIMATION dataset


Contains 11 new objects as shown below

![alt text](moped_objects.png)

The states the following for generating images in MOPED

* First uses KinectFusion to register frames from a single capture and then use a combination of manual annotations and
automatic registratiosn to align separate captures. They used
a 2016 paper to generate segmentation maps, we will use Ultralytics YOLOv8 or YOLOv11 to do the same for us.

## Procedure for adding new objects to the network

Step 1: Get a few pictures and calculate relative poses: How??

