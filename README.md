# MonoFlex
Released code for Objects are Different: Flexible Monocular 3D Object Detection, CVPR21

The README is still in progress :/

## Installation
This repo is tested with Ubuntu 20.04, python==3.7, pytorch==1.4.0 and cuda==10.1

```bash
conda create -n monoflex python=3.7

conda activate monoflex
```

Install PyTorch and other dependencies:

```bash
conda install pytorch==1.4.0 torchvision==0.5.0 cudatoolkit=10.1 -c pytorch

pip install -r requirements.txt
```

Build DCNv2 and the project
```bash
cd models/backbone/DCNv2

. make.sh

cd ../../..

python setup develop
```

## Data Preparation
Please download [KITTI dataset](http://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=3d) and organize the data as follows:

```
#ROOT
  |data/
    |KITTI/
      |ImageSets/ [already provided in this repo]
      |object/			
        |training/
          |calib/
          |image_2/
          |label/
        |testing/
          |calib/
          |image_2/
```

Then modify the paths in config/paths_catalog.py according to your data path.

### Training & Evaluation

Training with one GPU: (TODO: multi-GPU training will be further tested)

```bash
CUDA_VISIBLE_DEVICES=0 python tools/plain_train_net.py --batch_size 8 --config runs/monoflex.yaml --output output/exp
```

The model will be evaluated every two epochs (can be adjusted in the CONFIG) during training and you can also evaluate a checkpoint with

```bash
CUDA_VISIBLE_DEVICES=0 python tools/plain_train_net.py --config runs/monoflex.yaml --ckpt YOUR_CKPT  --eval
```

You can also specify --vis when evaluation to visualize the predicted heatmap and 3D bounding boxes.


## Acknowlegment

The code is heavily borrowed from [SMOKE](https://github.com/lzccccc/SMOKE) and thanks for their contribution.