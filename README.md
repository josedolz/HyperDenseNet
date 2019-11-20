# HyperDenseNet
- A new pytorch version has been implemented [here](https://github.com/josedolz/HyperDenseNet_pytorch)

This repository will contain the code of HyperDenseNet, a hyper-densely connected CNN to segment medical images in multi-modal image scenarios.

Among others, this network is ranked first in the MRBrainS MICCAI Challenge http://mrbrains13.isi.uu.nl/results.php


If you find that this work has been useful for your research, please consider citing the following works:

- Dolz J, Gopinath K, Yuan J, Lombaert H, Desrosiers C, Ben Ayed I. "[HyperDense-Net: A hyper-densely connected CNN for multi-modal image segmentation."](https://www.ncbi.nlm.nih.gov/pubmed/30387726) IEEE TMI. 2018 Oct 30.[Link](https://ieeexplore.ieee.org/abstract/document/8515234)

- Dolz J, Desrosiers C, Wang L, Yuang J, Shen D, Ben Ayed I. "[Isointense Infant Brain Segmentation with a Hyper-dense Connected Convolutional Neural Network"](https://pdfs.semanticscholar.org/32b9/b7c7b562bd60d6c2c3ce8c0c911a18f21654.pdf). IEEE International Symposium on Biomedical Imaging (ISBI), 616-620

A detail of a section of the proposed HyperDenseNet.
<br>
<img src="https://github.com/josedolz/HyperDenseNet/blob/master/Images/HyperDenseNet_Module.png"/>
<br>


## Content
- [Requirements](#requirements)
- [Training](#training)
- [Testing](#testing)
- [Versions](#versions)
- [Some results](#results)



## Requirements

- The code has been written in Python (2.7) and requires [Theano](http://deeplearning.net/software/theano/)
- You should also have installed [scipy](https://www.scipy.org/)
- (Optional) The code allows to load images in Matlab and Nifti formats. If you wish to use nifti formats you should install [nibabel](http://nipy.org/nibabel/) 
- Since, as you might now, sharing medical data is not a good-practice, I did not include any sample in the corresponding folders. To make your experiments you must include your data in the repositories indicated in the config file (LiviaNET_Config.ini and LiviaNET_Segmentation.ini)

## Running the code

Running the code actually works in the same way that LiviaNet. Just a reminder if you do not want to check the documentation from that net :)

## Training

### How do I train my own architecture from scratch?

To start with your own architecture, you have to modify the file "LiviaNET_Config.ini" according to your requirements.

Then you simply have to write in the command line:

```
THEANO_FLAGS='device=cuda0,floatX=float32,lib.cnmem=1' python ./networkTraining.py ./HyperDenseNet_Config.ini 0
```

This will save, after each epoch, the updated trained model.

If you use GPU, after nearly 5 minutes you will have your trained model from the example.

### Can I re-start the training from another epoch?

Imagine that after two days of training your model, and just before you have your new model ready to be evaluated, your computer breaks down. Do not panic!!! You will have only to re-start the training from the last epoch in which the model was saved (Let's say epoch 20) as follows:

```
python ./networkTraining.py ./HyperDenseNet_Config.ini 1 ./outputFiles/HyperDenseNet/Networks/HyperDenseNet_Epoch20
```

### Ok, cool. And what about employing pre-trained models?

Yes, you can also do that. Instead of loading a whole model, which limits somehow the usability of loading pre-trained models, this code allows to load weights for each layer independently. Therefore, weights for each layer have to be saved in an independent file. In its current version (v1.0) weights files must be in numpy format (.npy).

For that you will have to specify in the "LiviaNET_Config.ini" file the folder where the weights are saved ("weights folderName") and in which layers you want to use transfer learning ("weights trained indexes").

## Testing

### How can I use a trained model?

Once you are satisfied with your training, you can evaluate it by writing this in the command line:

```
python ./networkSegmentation.py ./HyperDenseNet_Segmentation.ini ./outputFiles/HyperDenseNet/Networks/HyperDenseNet_EpochX
```
where X denotes the last (or desired) epoch in which the model was saved.

### Versions
- Version 1.0. 
  * April,17th. 2018
    * HyperDenseNet processes multi-modal data in different branches which are densely connected (**so far only two-modalities**).
    

## Results

These images depicts some results included in the HyperDenseNet papers.


* Some qualitative results of the proposed HyperDenseNet compared to some baselines.
<br>
<img src="https://github.com/josedolz/HyperDenseNet/blob/master/Images/iSEG_Images.png"/>
<br>

* Analysis of features reuse in the case of two image modalities.
<br>
<img src="https://github.com/josedolz/HyperDenseNet/blob/master/Images/WeightsNorm_1_0.png"/>
<br>
