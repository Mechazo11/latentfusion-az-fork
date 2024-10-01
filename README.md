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


## Changelogs

TODO


## Setup:

* Install miniforge as shown here: https://github.com/conda-forge/miniforge

* Create the ```latentfusion``` environment: ```environment_updated.yml``` file: ```mamba env create -n latentfusion -f environment_updated.yml```

* Activate env using the shell script: ```source env.sh```. It ensures this directory is added to the ```$PYTHONPATH``` variable.

* Install pytorch with cuda support: ```mamba install pytorch torchvision torchaudio pytorch-cuda=12.4 -c pytorch -c nvidia```

* Test to make sure CUDA is found

```bash
python3
import torch
torch.cuda.is_available()
```

