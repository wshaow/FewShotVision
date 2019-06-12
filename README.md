# Few Shot Learning

## Enviroment
 - Python3
 - [Pytorch](http://pytorch.org/) 1.1
 - CUDA 10

## Getting started

### Installation

Git clone the repo:

```
git clone git@github.com:sicara/FewShotLearning.git
```

Then `cd FewShotLearning` and install virtualenv:

```
virtualenv venv --python=python3
source venv/bin/activate
```

Then install dependencies. If you are on linux run `pip install -r dev_requirements.txt`. If you are on macOS
run `pip install -r dev_requirements_macOS.txt`

### CUB
* run `source ./scripts/downloaders/download_CUB.sh`
You will need wget for that script.

### mini-ImageNet
* run `source ./scripts/downloaders/download_miniImagenet.sh`

(WARNING: This would download the 155G ImageNet dataset.) The compress file of mini-ImageNet is on muaddib.

### Self-defined setting
* Require three data split json file: 'base.json', 'val.json', 'novel.json' for each dataset  
* The format should follow   
{"label_names": ["class0","class1",...], "image_names": ["filepath1","filepath2",...],"image_labels":[l1,l2,l3,...]}  
See test.json for reference
* Put these file in the same folder and change data_dir['DATASETNAME'] in configs.py to the folder path  

## Run
To launch an experiment, run :
```
run-pipeline pipelines/run_experiment.yaml 
```
All the parameters of the experiment (dataset, backbone, method, number of examples per class ...) can be customized in the pipeline.

## Outputs \& results
You can find the outputs of your experiment in `./output/{dataset}/{method}_{backbone}/`
- The `.tar` files contain the state of the trained model after different number of epochs. `best_model.tar` contains the model with the best validation accuracy, which is used for evaluation.
- The `.hdf5` file contains the features vector of all images in the evaluation dataset, along with their labels.

Notes:
- Baseline and baseline++ don't save a `best_model.tar` file, and use the model with the highest number of epochs for evaluation.
- MAML-like algorithms don't save feature vectors.
 

## References
This code is modified from https://github.com/wyharveychen/CloserLookFewShot.

Their code was using modified and integrated code from:

* Framework, Backbone, Method: Matching Network
https://github.com/facebookresearch/low-shot-shrink-hallucinate 
* Omniglot dataset, Method: Prototypical Network
https://github.com/jakesnell/prototypical-networks
* Method: Relational Network
https://github.com/floodsung/LearningToCompare_FSL
* Method: MAML
https://github.com/cbfinn/maml  
https://github.com/dragen1860/MAML-Pytorch  
https://github.com/katerakelly/pytorch-maml
