# GeneBody benchmark - Deferred Neural Rendering: Image Synthesis using Neural Textures

GeneBody Benchmark reivison of the implementation of paper "Deferred Neural Rendering: Image Synthesis using Neural Textures", Siggraph 2019. This repository borrows most of the code from the [Unoffical original implementation](https://github.com/SSRSGJYD/NeuralTexture).



## Installation
The code is tested with Python3.7, PyTorch == 1.2 and CUDA == 10.0. We recommend you to use [anaconda](https://www.anaconda.com/) to make sure that all dependencies are in place. To create an anaconda environment:
```
conda env create -f environment.yml
conda activate neuraltexture
pip install -r requirements.txt
```


## File Organization

The root directory contains several subdirectories and files:

```
dataset/ --- custom PyTorch Dataset classes for loading included data
model/ --- custom PyTorch Module classes
util.py --- useful procedures
genebody/
  genebody_dataset.py --- genebody dataloader
  render_genebody.py --- render from RGB texture or neural texture
  train_genebody.py --- optimize genebody texture and U-Net jointly
zju/
  ...
```


## How to Use

### 1. Prepare datasets
```
├──data/
  ├──genebody/
    ├──amanda/
    ├──barry/
```
Please first `cd data/`, and then download datasets into `data/`. The organization of the datasets should be the same as above.


### 2. Render SMPLx UV images
NeuralTexture requires the per-view UV data as the input of network, and take render `amanda` as an example, run
```powershell
python render_uv.py --datatype genebody --datadir path_to_genebody/amanda --workers 8
```
Then, in amanda/smpl_uv, the code generates per-view UV rendered images in EXR format.

### 3. Train GeneBody

```powershell
python genebody/train_genebody.py --data path_to_genebody --subject amanda
```

### 4. Render GeneBody
```powershell
python genebody/render_genebody.py --data path_to_genebody --subject amanda
```

## Citation
If you find this repo is useful for your research, please cite the following papers
```
@article{
    author = {Wei, Cheng and Su, Xu and Jingtan, Piao and Wayne, Wu and Chen, Qian and Kwan-Yee, Lin and Hongsheng, Li},
    title = {Generalizable Neural Performer: Learning Robust Radiance Fields for Human Novel View Synthesis},
    publisher = {arXiv},
    year = {2022},
  }

@article{thies2019deferred,
  title={Deferred neural rendering: Image synthesis using neural textures},
  author={Thies, Justus and Zollh{\"o}fer, Michael and Nie{\ss}ner, Matthias},
  journal={ACM Transactions on Graphics (TOG)},
  volume={38},
  number={4},
  pages={1--12},
  year={2019},
  publisher={ACM New York, NY, USA}
}
```

