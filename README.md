# ComfyUI wrapper node for "champ"
## WORK IN PROGRESS

![image](https://github.com/kijai/ComfyUI-champWrapper/assets/40791699/cacc7067-19ec-4292-a809-7f3a2b660d1c)

These checkpoints go in the `ComfyUI/custom_nodes/ComfyUI-champWrapper/checkpoints` -folder:

https://drive.google.com/drive/folders/1hZiOHG-qDf0Pj7tvfxC70JQ6wHUvUDoY

And this model along with it's config go in the `ComfyUI/custom_nodes/ComfyUI-champWrapper/checkpoints/image_encoder`:

https://huggingface.co/lambdalabs/sd-image-variations-diffusers/tree/main/image_encoder


# Original repo:

<h1 align='Center'>Champ: Controllable and Consistent Human Image Animation with 3D Parametric Guidance</h1>

<div align='Center'>
    <a href='https://github.com/ShenhaoZhu' target='_blank'>Shenhao Zhu</a><sup>*1</sup>&emsp;
    <a href='https://github.com/Leoooo333' target='_blank'>Junming Leo Chen</a><sup>*2</sup>&emsp;
    <a href='https://github.com/daizuozhuo' target='_blank'>Zuozhuo Dai</a><sup>3</sup>&emsp;
    <a href='https://ai3.fudan.edu.cn/info/1088/1266.htm' target='_blank'>Yinghui Xu</a><sup>2</sup>&emsp;
    <a href='https://yoyo000.github.io/' target='_blank'>Yao Yao</a><sup>1</sup>&emsp;
    <a href='http://zhuhao.cc/home/' target='_blank'>Hao Zhu</a><sup>+1</sup>&emsp;
    <a href='https://sites.google.com/site/zhusiyucs/home' target='_blank'>Siyu Zhu</a><sup>+2</sup>
</div>
<div align='Center'>
    <sup>1</sup>Nanjing University <sup>2</sup>Fudan University <sup>3</sup>Alibaba Group
</div>
<div align='Center'>
    <sup>*</sup>Equal Contribution
    <sup>+</sup>Corresponding Author
</div>

<div align='Center'>
    <a href='https://fudan-generative-vision.github.io/champ/#/'><img src='https://img.shields.io/badge/Project-Page-Green'></a>
    <a href='https://arxiv.org/abs/2403.14781'><img src='https://img.shields.io/badge/Paper-Arxiv-red'></a>
    <a href='https://youtu.be/2XVsy9tQRAY'><img src='https://badges.aleen42.com/src/youtube.svg'></a>
</div>

https://github.com/fudan-generative-vision/champ/assets/82803297/b4571be6-dfb0-4926-8440-3db229ebd4aa

# Framework
![framework](assets/framework.jpg)

# Installation
- System requirement: Ubuntu20.04
- Tested GPUs: A100

Create conda environment: 
```bash
  conda create -n champ python=3.10
  conda activate champ
```
Install packages with `pip`:
```bash
  pip install -r requirements.txt
```

# Download pretrained models

1. Download pretrained weight of base models: 
    - [StableDiffusion V1.5](https://huggingface.co/runwayml/stable-diffusion-v1-5)
    - [sd-vae-ft-mse](https://huggingface.co/stabilityai/sd-vae-ft-mse)
    - [image_encoder](https://huggingface.co/lambdalabs/sd-image-variations-diffusers/tree/main/image_encoder)

2. Download our checkpoints: \
Our [checkpoints](https://drive.google.com/drive/folders/1hZiOHG-qDf0Pj7tvfxC70JQ6wHUvUDoY?usp=sharing) consist of denoising UNet, guidance encoders, Reference UNet, and motion module.

Finally, these pretrained models should be organized as follows:

```text
./pretrained_models/
|-- champ
|   |-- denoising_unet.pth
|   |-- guidance_encoder_depth.pth
|   |-- guidance_encoder_dwpose.pth
|   |-- guidance_encoder_normal.pth
|   |-- guidance_encoder_semantic_map.pth
|   |-- reference_unet.pth
|   `-- motion_module.pth
|-- image_encoder
|   |-- config.json
|   `-- pytorch_model.bin
|-- sd-vae-ft-mse
|   |-- config.json
|   |-- diffusion_pytorch_model.bin
|   `-- diffusion_pytorch_model.safetensors
`-- stable-diffusion-v1-5
    |-- feature_extractor
    |   `-- preprocessor_config.json
    |-- model_index.json
    |-- unet
    |   |-- config.json
    |   `-- diffusion_pytorch_model.bin
    `-- v1-inference.yaml
```

# Inference
We have provided several sets of [example data](https://drive.google.com/file/d/1-sJlnnZu-nTNTvRtvFVr_y-2_CA5-_Yz/view?usp=sharing) for inference. Please first download and place them in the `example_data` folder. 
Here is the command for inference:
```bash
  python inference.py --config configs/inference.yaml
```
Animation results will be saved in `results` folder. You can change the reference image or the guidance motion by modifying `inference.yaml`. 

You can also extract the driving motion from any videos and then render with Blender. We will later provide the instructions and scripts for this.

# Acknowledgements
We thank the authors of [MagicAnimate](https://github.com/magic-research/magic-animate), [Animate Anyone](https://github.com/HumanAIGC/AnimateAnyone), and [AnimateDiff](https://github.com/guoyww/AnimateDiff) for their excellent work. Our project is built upon [Moore-AnimateAnyone](https://github.com/MooreThreads/Moore-AnimateAnyone), and we are grateful for their open-source contributions.

# Citation
If you find our work useful for your research, please consider citing the paper:
```
@misc{zhu2024champ,
      title={Champ: Controllable and Consistent Human Image Animation with 3D Parametric Guidance}, 
      author={Shenhao Zhu and Junming Leo Chen and Zuozhuo Dai and Yinghui Xu and Xun Cao and Yao Yao and Hao Zhu and Siyu Zhu},
      year={2024},
      eprint={2403.14781},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
```
