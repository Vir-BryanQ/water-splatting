<p align="center">
    <h1>
        <span class="title-main"><span>WaterSplatting</span></span>
        <span class="title-small">Fast Underwater 3D Scene Reconstruction Using Gaussian Splatting</span>
      </h1>
  <p align="center">
    <a>Huapeng Li</a>
    ·
    <a>Wenxuan Song</a>
    ·
    <a>Tianao Xu</a>
    ·
    <a>Alexandre Elsig</a>
    ·
    <a>Jonas Kulhanek</a>
  </p>
  <h3 align="center"><a href="https://arxiv.org/pdf/2408.08206">📄 Paper</a> | <a href="https://water-splatting.github.io/">🌐 Project Page</a></h3>
  <div align="center"></div>
</p>
<br/>
<style>
      .video.teaser-video::before {
        padding-bottom: 50%;
      }
    </style>
    <video class="video" style="aspect-ratio: 1920/1080" loop muted autoplay>
      <source src="/.assets/curasao.webm" type="video/webm">
      <source src="/.assets/curasao.mp4" type="video/mp4">
    </video>
    <p class="justify" style="font-size: 1rem;margin: 0 0 0.4rem 0; text-align-last: center">
    <strong>WaterSplatting</strong> combines 3DGS with volume rendering to enable water/fog modeling</strong>
    </p>
<p align="justify">
We introduce WaterSplatting, a novel approach that fuses volumetric rendering with 3DGS to handle underwater data effectively. 
Our method employs 3DGS for explicit geometry representation and a separate volumetric field (queried once per pixel) for capturing the scattering medium. 
This dual representation further allows the restoration of the scenes by removing the scattering medium. 
Our method outperforms state-of-the-art NeRF-based methods in rendering quality on the underwater SeaThru-NeRF dataset. 
Furthermore, it does so while offering real-time rendering performance.
</p>
<br>

## Installation

Our method is based on [nerfstudio](https://docs.nerf.studio/index.html).

### Install nerfstudio
#### Create environment
```bash
conda create --name water_splatting -y python=3.8
conda activate water_splatting
python -m pip install --upgrade pip
```
#### PyTorch
```bash
pip uninstall torch torchvision functorch tinycudann

pip install torch==2.1.2+cu118 torchvision==0.16.2+cu118 --extra-index-url https://download.pytorch.org/whl/cu118
```

#### Install tiny-cuda-nn
```bash
pip install ninja git+https://github.com/NVlabs/tiny-cuda-nn/#subdirectory=bindings/torch
```

#### Install nerfstudio
```bash
pip install nerfstudio
ns-install-cli
```

### Local installation
```bash
git clone git@github.com:water-splatting/water-splatting.git
cd water_splatting

conda activate water_splatting
pip install -e .
```

## Training
To start the training on the [SeaThru-NeRF]() dataset, run the following commands:
```bash
cd /your_path_to_dataset/SeathruNeRF_dataset/IUI3-RedSea
mkdir colmap
mv sparse colmap/
```

Then, run the following commands for training:
```bash
cd /your_path_to_repo/water_splatting
ns-train water-splatting --vis viewer+wandb colmap --data /your_path_to_dataset/SeathruNeRF_dataset/IUI3-RedSea --images-path images_wb
```

## Interactive viewer
To start the viewer and explore the trained models, run one of the following:
```bash
ns-viewer --load-config outputs/unnamed/water-splatting/your_timestamp/config.yml
```

## Rendering videos
To render a video on a trajectory (e.g., generated from the interactive viewer), run:
```bash
ns-render camera-path --load-config outputs/unnamed/water-splatting/your_timestamp/config.yml --camera-path-filename /your_path_to_dataset/SeathruNeRF_dataset/IUI3-RedSea/camera_paths/your_trajectory.json --output-path renders/IUI3-RedSea/water_splatting.mp4
```

## Rendering dataset
To render testing set for a checkpoint, run:
```bash
ns-render dataset --load-config outputs/unnamed/water-splatting/your_timestamp/config.yml --data /your_path_to_dataset/SeathruNeRF_dataset/IUI3-RedSea
```
</p>
</section>

## Acknowledgements
This work was supported by the Czech Science Foundation (GACR) EXPRO (grant no. 23-07973X), and by the Ministry of Education, Youth and Sports of the Czech Republic through the e-INFRA CZ (ID:90254).
Jonas Kulhanek acknowledges travel support from the European Union’s Horizon 2020 research and innovation programme under ELISE (grant no. 951847).

## Citation
If you find our code or paper useful, please cite:
```bibtex
@article{li2024watersplatting,
  title={{W}ater{S}platting: Fast Underwater {3D} Scene Reconstruction using Gaussian Splatting},
  author={Li, Huapeng and Song, Wenxuan and Xu, Tianao and Elsig, Alexandre and Kulhanek, Jonas},
  journal={arXiv},
  year={2024}
}
```
