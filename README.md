# Make Your Own Sprites: Aliasing-Aware and Cell-Controllable Pixelization


## Description
This is the official implementation of the SIGGRAPH Asia 2022 paper "Make Your Own Sprites: Aliasing-Aware and Cell-Controllable Pixelization". Paper can be found at [here](https://dl.acm.org/doi/pdf/10.1145/3550454.3555482).

## Video Demo
Please see our [video demo](https://youtu.be/ElpXLF8nY1c) on YouTube.

## Prerequisites
- Linux
- Python 3
- NVIDIA GPU + CUDA CuDNN + 20GB GPU RAM
- CUDA 11.6 + cuDnn

## Dataset
The dataset is available at https://drive.google.com/file/d/1YAjcz6lScm-Gd2C5gj3iwZOhG5092fRo/view?usp=sharing.

## Pretrained Models
| Path | Description
| :--- | :----------
|[Structure Extractor](https://drive.google.com/file/d/1VRYKQOsNlE1w1LXje3yTRU5THN2MGdMM/view?usp=sharing) | A VGG-19 model pretrained on Multi-cell dataset.
|[AliasNet](https://drive.google.com/file/d/17f2rKnZOpnO9ATwRXgqLz5u5AZsyDvq_/view?usp=sharing) | An encoder-decoder network pretrained on Aliasing dataset.
|[I2PNet](https://drive.google.com/file/d/1i_8xL3stbLWNF4kdQJ50ZhnRFhSDh3Az/view?usp=sharing) | I2PNet.
|[P2INet](https://drive.google.com/file/d/1z9SmQRPoIuBT_18mzclEd1adnFn2t78T/view?usp=sharing) | P2INet.

## Env
Use Anaconda3 to add the env `CondaEnv_CUDA11.6.yaml`

## Train
Download the dataset. Create two empty directories ./datasets/TRAIN_DATA/trainA and ./datasets/TRAIN_DATA/trainB.

Put non-pixel art images in ./datasets/TRAIN_DATA/trainA and put multi-cell pixel arts in ./datasets/TRAIN_DATA/trainB.

Run `python -m visdom.server` first.

Run the following command to train:

`python train.py --gpu_ids 0 --batch_size 2 --preprocess none --dataroot ./datasets/TRAIN_DATA/ --name YOUR_MODEL_NAME`

The checkpoints and logs will be saved in ./checkpoints/YOUR_MODEL_NAME.

## Test
Create empty directory ./dataset/TEST_DATA/Input.

Put test images in ./dataset/TEST_DATA/Input, and run `python prepare_data.py` to prepare data.

Run `python -m visdom.server` first.

Run the following command to test:

`python test.py --gpu_ids 0 --batch_size 1 --preprocess none --num_test 4 --epoch WHICH_EPOCH --dataroot ./datasets/TEST_DATA/ --name YOUR_MODEL_NAME`

The result will be saved in ./result/YOUR_MODEL_NAME.

To use the pre-trained model, put `160_net_G_A.pth` and `160_net_G_B.pth` into `checkpoints\YOUR_MODEL_NAME`, then run:

``python test.py --gpu_ids 0 --batch_size 1 --preprocess none --num_test 4 --epoch 160 --dataroot ./datasets/TEST_DATA/ --name YOUR_MODEL_NAME``

## License
Software Copyright License for non-commercial scientific research purposes. Please read carefully the [terms and conditions](https://github.com/WuZongWei6/Pixelization/blob/main/LICENSE.md) in the LICENSE file and any accompanying documentation before you download and/or use the Pixel Art and/or Non-pixel art dataset, model and software, (the "Data & Software"), including code, images, videos, textures, software, scripts, and animations. By downloading and/or using the Data & Software (including downloading, cloning, installing, and any other use of the corresponding github repository), you acknowledge that you have read these terms and conditions, understand them, and agree to be bound by them. If you do not agree with these terms and conditions, you must not download and/or use the Data & Software. Any infringement of the terms of this agreement will automatically terminate your rights under this [License](https://github.com/WuZongWei6/Pixelization/blob/main/LICENSE.md).

## Acknowledgements
- The code adapted from [pytorch-CycleGAN-and-pix2pix](https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix) and [SCGAN](https://github.com/makeuptransfer/SCGAN).
- The dataset is collected from the Internet. Most of the pixel arts are from [eBoyArts](https://www.eboy.com/pool/everything/1).
