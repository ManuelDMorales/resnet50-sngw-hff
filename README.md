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
     |___ GenRelWf
          |___ Distance_1Kpc
          |___ Distance_5Kpc
          |___ Distance_10Kpc
     |___ PhenWf
|___ Metrics
     |___ kfold_CV
|___ Models
     |___ GridSearchCV
     |___ Single_learning
|___ LICENCE
|___ README.md
```

The codes were run in Google Colaboratory, in the following order:

`Convert_StrainImage.ipynb` for reading the window strain datasets and converting them into images of TF scalograms. In the current implementation, data can be loaded by two folders: PhenWf and GenRelWf for phenomenological waveforms and general relativistic waveforms, respectively. Moreover, for general relativistic waveforms, datasets are loaded for folders at different distances (see important instruction no. 1 of the next section).

`Apply_ResNet50.ipynb` for apply the ResNet50 model

# Important instructions

1. All scripts were run in a specific Google Drive location, then you will need to edit the high level path location in which the project (resnet50-sngw-hff) is located.
   
2. Notice that the Datasets folder, as shown in the project's tree, has a specific hierarchical estructure. Excepting the number of distances (which can be more or less than 3), it is highly recommended to maintain this structure, to have a reasonable organization of the datasets, and to run the `Convert_StrainImage.ipynb` script without path locations changes inside the folder of the project. Therefore, if you run codes datagen-sngw-phen and/or datagen-sngw-genrel to generate datasets, located output folders (syntax: detector_GPStime) inside the PhenWf folder and/or the GenRelWf/Distance_dKpc (with "d" the specific distance from the source), respectively.
