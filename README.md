# SSL-RGB2IR

This repository provides code for our paper:
 
[SSL-RGB2IR: Semi-supervised RGB-to-IR Image-to-Image Translation for Enhancing Vision Task Training in Semantic Segmentation and Object Detection
](link)

[Aniruddh Sikdar](https://www.linkedin.com/in/aniruddh-sikdar-723112b8/), [Qiranul Saadiyean*](https://www.linkedin.com/in/qsaddy/), [Prahlad Anand](https://www.linkedin.com/in/prahlad-anand), [Suresh Sundaram](https://aero.iisc.ac.in/people/suresh-sundaram/)

IROS 2024

 ### Contents

<div class="toc">
<ul>
<li><a href="#-ssl-rgb2ir">About</a></li>
<li><a href="#-setup">Setup</a></li>
<li><a href="#-experiments">Experiments</a></li>
<li><a href="#-checkpoints">Checkpoints</a></li>
</ul>
</div>

## About

The scarcity of annotated infrared (IR) image datasets limits deep learning networks from achieving per- formances comparable to those achieved with RGB data. To address this, we introduce a novel semi-supervised RGB- to-IR Image-to-Image Translation model (SSL-RGB2IR) that generates synthetic IR data from RGB images. Our model effectively preserves the IR characteristics in the generated images from both synthetic and real-world data. Compared to existing image-to-image translation techniques, training models on this generated IR data significantly improves performance in downstream tasks like segmentation and detection. Notably, in sim-to-real transfer, the segmentation model trained on SSL-RGB2IR generated IR images outperforms baselines and other Image-to-Image (I2I) models. Furthermore, for real-world applications utilizing EO/IR fusion images, this approach solves the well-known challenge of co-registering EO and IR images, which often have inherent misalignment’s due to differing sensor characteristics.

## Setup

1. First download and setup [Anaconda](https://docs.anaconda.com/anaconda/install/linux/) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html).
2. Create and activate a conda (anaconda / miniconda) environment
```
conda create -n ssl-rgb2ir -f environment.yaml
conda activate ssl-rgb2ir
```

3. Download M3FD, MSRS and MVSS datasets and format as follows:

## Experiments

#### Inferencing 

1. Pseudo-pair generation network
```
python3 inference_batch.py --input_folder /path/to/imgs --checkpoint /path/to/checkpoints/gen_00060000.pt --a2b 1 --seed 1 --num_style 1 --synchronized --output_only --config ./configs/tir2rgb_folder.yaml --output_folder /path/to/result
```

2. Secondary network
```
python test.py --dataroot /path/to/imgs --name experiment_name --CUT_mode CUT  --model cut --phase test --epoch latest --preprocess none
```

#### Training

1. Pseudo-pair generation network
```
python train.py --config configs/tir2rgb_folder_.yaml --output_path ./m3fd
```

2. Secondary network
```
python train.py --name experiment_name  --CUT_mode CUT --model semi_cut --dataroot /path/to/imgs --paired_dataroot /path/to/imgs --checkpoints_dir ./pretrained_models --dce_idt --lambda_VGG -1  --lambda_NCE_s 0.05 --use_curriculum  --gpu_ids 0
```

## Checkpoints

[Coming Soon]


## Cite

Please cite our work if you find it useful:
```
@inproceedings{2023iccv_PASTA, 
    author = {Sikdar, Aniruddh and Saadiyean, Qiranul and Anand, Prahlad and Sundaram, Suresh},
    title = {SSL-RGB2IR: Semi-supervised RGB-to-IR Image-to-Image Translation for Enhancing Vision Task Training in Semantic Segmentation and Object Detection},
    year = 2024,
    booktitle = {IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS)}
}
```
