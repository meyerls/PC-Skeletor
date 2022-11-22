# PC Skeletor - Point Cloud Skeletonization <img align="right" height="200" src="img/PCSkeletor.png">

<a href="https://img.shields.io/pypi/pyversions/pc_skeletor"><img alt="PyPI - Python Version" src="https://img.shields.io/pypi/pyversions/pc_skeletor"></a>
<a href="https://github.com/meyerls/PC-Skeletor/actions"><img alt="GitHub Workflow Status" src="https://img.shields.io/github/workflow/status/meyerls/PC-Skeletor/Python%20package"></a>
<a href="https://github.com/meyerls/PC-Skeletor/blob/main/LICENSE"><img alt="license" src="https://img.shields.io/github/license/meyerls/PC-Skeletor"></a>

## About

PC Skeletor is a Python library for extracting a 1d skeleton from 3d point clouds using the algorithm from
[Laplacian-Based Contraction](https://taiya.github.io/pubs/cao2010cloudcontr.pdf) or
[L1-Medial Skeleton](https://www.cs.sfu.ca/~haoz/pubs/huang_sig13_l1skel.pdf) (Not yet implemented!).


<p align="center">
    <img width="70%" src="img/tree_sceleton_small.gif">
</p>

## Installation

Make sure that you have a Python version >=3.7 installed.

This repository is tested on Python 3.6+ and can currently only be installed
from [TestPyPi](https://test.pypi.org/project/pc-skeletor/).

 ````bash
pip install -i https://test.pypi.org/simple/ pc-skeletor
 ````

## Usage

````python
import pc_skeletor
from pc_skeletor import skeletor
from pc_skeletor.download import Dataset
import numpy as np

# Download test tree dataset
downloader = Dataset()
downloader.download_tree_dataset()

# Init tree skeletonizer
skeletor = skeletor.Skeletonizer(point_cloud=downloader.file_path,
                                 down_sample=0.01,
                                 debug=False)
sceleton = skeletor.extract(method='Laplacian')
# save results
skeletor.save(result_folder='./data/')
# Make animation of original point cloud and skeleton
skeletor.animate(init_rot=np.asarray([[1, 0, 0],
                                      [0, 0, 1],
                                      [0, 1, 0]]), steps=200, out='./data/')
````

## Literature and Code used for implementation

#### Laplacian based contraction

Our implementation
of [Point Cloud Skeletons via Laplacian-Based Contraction](https://taiya.github.io/pubs/cao2010cloudcontr.pdf) is a
python reimplementation of the original [Matlab code](https://github.com/taiya/cloudcontr).

#### L1-Medial Skeleton of Point Cloud (NOT YET IMPLEMENTED!)

Paper: https://www.cs.sfu.ca/~haoz/pubs/huang_sig13_l1skel.pdf

Source Code: https://github.com/HongqiangWei/L1-Skeleton

````bash
@ARTICLE{Huang2013,
title = {L1-Medial Skeleton of Point Cloud},
author = H. Huang and S. Wu and D. Cohen-Or and M. Gong and H. Zhang and G. Li and B.Chen},
journal = {ACM Transactions on Graphics},
volume = {32},
issue = {4},
pages = {65:1--65:8},
year = {2013}
}
````

#### Robust Laplacian for Point Clouds

Computation of the discrete laplacian operator
via [Nonmanifold Laplace](http://www.cs.cmu.edu/~kmcrane/Projects/NonmanifoldLaplace/NonmanifoldLaplace.pdf) can be
found in the [robust-laplacians-py](https://github.com/nmwsharp/robust-laplacians-py) repository.

## Limitation / Improvements

- [ ] Implement L1-Medial skeleton of point cloud
- [ ] Improve code
- [ ] Provide example
- [ ] Adapt hyperparameters for laplacian based contraction
- [ ] Test code