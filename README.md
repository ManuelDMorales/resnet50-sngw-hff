# Summary

Deep residual network (ResNet50) to classify RGB images of time-frequency (TF) Morlet wavelet scalograms of gravitational waves from core-collapse supernovae (CCSNe). We performed a three-class classification, in which the target label is assigned if the slope of the High Frequency Feature, present in the scalograms, belongs to one of three slope ranges. This three-class classification allows us to study the detectability of the HFF because, depending on the CCSN model and the noise realization, the visibility of the HFF can vary.

This project draws on datasets generated in projects [datagen-sngw-phen](https://github.com/ManuelDMorales/datagen-sngw-phen) and [datagen-sngw-genrel](https://github.com/ManuelDMorales/datagen-sngw-genrel), which consist of window strain time series containing interferometric noise plus gravitational waves from CCSNe. Jupyter notebooks developed in Python by Manuel D. Morales (e-mail: <manueld.morales@academicos.udg.mx>).

# Science background

The samples used in this project consist of time series of real noise from LIGO (L1, H1) and (V1) interferometric detectors from the O3b run plus gravitational wave signals from CCSN, bot phenomenological waveforms, and general relativistic waveforms. In all cases, these waveforms contain the HFF which, depending on the model and the noise, is more or less visible.

Phenomenological waveforms come from a stochastic non-physical model that mimics the HFF, see [Astone et al Phys. Rev. D 98, 122002 (2018)](https://doi.org/10.1103/PhysRevD.98.122002). On the other hand, general relativistic waveforms are a modified version of those obtained from three multidimensional CCSN simulations: [Andresen 2019 m15nr h+](https://doi.org/10.1093/mnras/stz990), [Morozova 2018 M13_SFHo h+](https://doi.org/10.3847/1538-4357/aac5f1), and [Cerda-Duran 2013 fiducial h+](https://iopscience.iop.org/article/10.1088/2041-8205/779/2/L18). The modification of the general relativistic waveforms has to do with the fact that all features other than the HFF were removed or filtered.

The three target labels for the classification are defined as follows:

- Class 1:  1,620 =< HFF slope =< 4,990
- Class 2: 1,450 =< HFF slope < 1,620
- Class 3: 950 =< HFF slope < 1,450

Fig. 1 Shows the ResNet50 architecture used in this project, which consists of 50 layers in the main path, and 23,593,859 model parameters occupying 90MB in memory.

# Implementation structure

```
resnet50-sngw-hff
|___ Codes
     |___ Convert_StrainImage.ipynb
     |___ Apply_ResNet50.ipynb
|___ Datasets
|___ Metrics
     |___ kfold_CV
|___ Models
     |___ GridSearchCV
     |___ Single_learning
|___ LICENCE
|___ README.md
```

The codes were run in Google Colaboratory, in the following order:

`Convert_StrainImage.ipynb` for reading the window strain datasets and converting them into images of TF scalograms.

`Apply_ResNet50.ipynb` for apply the ResNet50 model

# Important instructions
