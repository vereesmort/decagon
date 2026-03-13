# Decagon: Representation Learning on Multimodal Graphs

#### Author: [Marinka Zitnik](http://stanford.edu/~marinka) (marinka@cs.stanford.edu)

#### [Project website](http://snap.stanford.edu/decagon)

## Overview

This repository contains code necessary to run the Decagon algorithm. Decagon is a method for learning node 
embeddings in multimodal graphs, and is especially useful for link prediction in highly multi-relational settings. See 
our [paper](https://doi.org/10.1093/bioinformatics/bty294) for details on the algorithm.
  
## Usage: Polypharmacy

Decagon is used to address a burning question in pharmacology, which is that of predicting 
[safety of drug combinations](http://stanford.edu/~marinka/slides/decagon-ismb18.pdf). 

We construct a multimodal graph of protein-protein interactions, drug-protein target interactions, and 
polypharmacy side effects, which are represented as drug-drug interactions, where each side effect is an edge of a 
different type. 

<p align="center">
<img src="https://github.com/marinkaz/decagon/blob/master/images/polypharmacy-graph.png" width="600" align="center">
</p>

Decagon uses graph convolutions to embed the multimodal graph in a compact vector space and then uses
the learned embeddings to predict side effects of drug combinations. 
  
<p align="center">
<img src="https://github.com/marinkaz/decagon/blob/master/images/decagon-architecture-1.png" width="800" align="center">
</p>

### Running the code

The setup for the polypharmacy problem on a synthetic dataset is outlined in `main.py`. It uses a small synthetic 
network example with five edge types. Run the code as following:

    $ python main.py
    
The full polypharmacy dataset (described in the paper) is available on the 
[project website](http://snap.stanford.edu/decagon). To run the code on the full dataset first download all data files
from the [project website](http://snap.stanford.edu/decagon). The polypharmacy dataset is already preprocessed and ready to use. 
After cloning the project, replace the synthetic example in `main.py` with the polypharmacy dataset and run the model.  

### Dataset

You can Download the real dataset on the [project website](http://snap.stanford.edu/decagon). Creat a data folder. put the data
on this folder and unzip the data. There should be six .csv files on the data folder. 


## Citing

If you find *Decagon* useful for your research, please consider citing [this paper](https://academic.oup.com/bioinformatics/article/34/13/i457/5045770):

    @article{Zitnik2018,
      title     = {Modeling polypharmacy side effects with graph convolutional networks.},
      author    = {Zitnik, Marinka and Agrawal, Monica and Leskovec, Jure},
      journal   = {Bioinformatics},
      volume    = {34},
      number    = {13},
      pages     = {457–466},
      year      = {2018}
    }

## Miscellaneous

Please send any questions you might have about the code and/or the 
algorithm to <marinka@cs.stanford.edu>.

This code implements several different edge decoders (innerproduct, distmult, 
bilinear, dedicom) and loss functions (hinge loss, cross entropy). Many deep variants are possible and what works 
best might depend on a concrete use case.  

## Requirements

Decagon is tested to work under Python 2 and Python 3. 

Recent versions of Tensorflow, sklearn, networkx, numpy, and scipy are required. All the required packages can be installed using the following command:

    $ pip install -r requirements.txt

## License

Decagon is licensed under the MIT License.



## Log TensorFlow 2.x upgrade
1. Updated requirements.txt
Upgraded TensorFlow from 1.8.0 to >=2.8.0,<3.0.0
Updated related dependencies (numpy, scikit-learn, scipy, networkx, tensorboard)
Removed Python 2-only packages (enum34, funcsigs, backports.weakref)
2. Updated decagon/deep/optimizer.py
Changed tf.app.flags → tf.compat.v1.app.flags
Changed tf.train.AdamOptimizer → tf.compat.v1.train.AdamOptimizer
Changed tf.op_scope → tf.compat.v1.name_scope
Fixed error message typo ('params' → 'indices')
3. Updated decagon/deep/model.py
Changed tf.app.flags → tf.compat.v1.app.flags
Changed tf.variable_scope → tf.compat.v1.variable_scope
Changed tf.get_collection → tf.compat.v1.get_collection
Changed tf.GraphKeys.GLOBAL_VARIABLES → tf.compat.v1.GraphKeys.GLOBAL_VARIABLES
4. Updated decagon/deep/layers.py
Changed tf.app.flags → tf.compat.v1.app.flags
Changed tf.random_uniform → tf.random.uniform
Changed tf.sparse_retain → tf.sparse.retain
Changed tf.variable_scope → tf.compat.v1.variable_scope (5 occurrences)
Changed tf.sparse_tensor_dense_matmul → tf.sparse.sparse_dense_matmul (3 occurrences)
5. Updated decagon/deep/inits.py
Changed tf.random_uniform → tf.random.uniform
6. Updated main_real_data.py
Added tf.compat.v1.disable_v2_behavior() after TensorFlow import
Changed tf.app.flags → tf.compat.v1.app.flags
Changed all tf.placeholder → tf.compat.v1.placeholder
Changed tf.placeholder_with_default → tf.compat.v1.placeholder_with_default
Changed tf.sparse_placeholder → tf.compat.v1.sparse_placeholder
Changed tf.Session → tf.compat.v1.Session
Changed tf.global_variables_initializer → tf.compat.v1.global_variables_initializer
7. Updated main.py
Same changes as main_real_data.py