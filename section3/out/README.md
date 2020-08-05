# Expected results

Please put the artefacts from Section 3 here:  
  
* Code that runs inference on a DICOM volume and produces a DICOM report
* A report.dcm file with a sample report
* Screenshots of your report shown in the OHIF viewer
* 1-2 page Validation Plan

## Suggestions for making your project stand out

* Can you propose a better way of filtering a study for correct series?
* Can you think of what would make the report you generate from your inference better? What would be the relevant information that you could present which would help a clinician better reason about whether your model performed well or not?
* Try to construct a fully valid DICOM as your model output (per [DICOM PS3.3#A8](http://dicom.nema.org/medical/dicom/current/output/html/part03.html#sect_A.8)) with all relevant fields. Construction of valid DICOM has a very calming effect on the mind and body.
* Try constructing a DICOM image with your segmentation mask as a separate image series so that you can overlay it on the original image using the clinical image viewer and inspect the predicted volume better. Note that OHIF does not support overlaying - try using Slicer 3D or Radiant (Fusion feature). Include screenshots.

## Summary and brief validation overview

Hippocampus is one of the major structures of the human brain with functions that are primarily connected to learning and memory. The volume of the hippocampus may change over time, with age, or as a result of disease. In order to measure hippocampal volume, a 3D imaging technique with good soft tissue contrast is
required. MRI provides such imaging characteristics, but manual volume measurement still requires careful and time consuming delineation of the hippocampal boundary. 

Intended use: 

The HippocampAI system is desinged to assist clinicians by predicting the volume of the Hippocampus for AZ progression assessment. 

Steps:

In this project we have go through the steps that typically can have steps for end to end implemention of 3D imaging platform to enable AI techniques to help clinicians assess hippocampal volume in an automated way and integrate this algorithm into a clinician’s working environment.

The project is broken into 3 logical phases: 


1. Using correct data from larger dataset 

We are using the "Hippocampus" dataset from the Medical Decathlon competition. This dataset is stored as a collection of NIFTI files, with one file per volume, and one file per corresponding segmentation mask. The original images here are T2 MRI scans of the full brain. As noted, in this dataset we are using cropped volumes where only the region around the hippocampus has been cut out. This makes the size of our dataset quite a bit smaller, our machine learning problem a bit simpler and allows us to have reasonable training times. You should not think of it as "toy" problem, though. Algorithms that crop rectangular regions of interest are quite common in medical imaging. Segmentation is still hard.

Section 1 deals with scanning all images and ensuring the volume of the images is between ~2200 and ~4500. The outliers are identified and curated dataset is presented to Section 2. 

2. 

In this section, we present the curated a hippocampal image dataset to train the U-net based segmentation model, and we capture performance on the test data. Then, you will connect the machine learning execution code. We use label data to train the model and validate on the test data. We plot training and accuracy metrics to ensure our accuracy is as per required range as specified by dice and jaccard scores. We used tensorboard to track training and validation chart visually. 

3. In section3, we simulate clinical environment with PAC and OHIF viewer application. We run our prediction on AI server where HippoVolume.AI resides with Unet model implemented in section2. We send predictions of volume in report.dcm and this report can be viewed in OHIF viewer. 

Specifically, validation plan for HippoVolume.AI should be based upon following considerations. 

1. ground truth -- this is the most important aspect of this system. In this system the CT scanned images taken as slices from human brain. The ground truth can be established by using tools such as slicer where labels can be created in each plane which can generate volumes of interest. 

2. quality of the images - identifying correct range of brightness and contrast can be key

3. modality - while this should not be a concern as most equipments in the clincal settings are 
calibrated, it is important to pay attention of there is a common issue from particular equipment of
a batch of equipment causing a problem. 

We can assume the U-net architecure for image segmentation is well tested but it is a good idea to
run prediction on a smaller unseen data to ensure the predictions are acceptable with desired accuracy. 

As part of the Algorithm validation, ground truth establishments, ability to detect outliers and testing volume predictions on unseen images should be undertaken. 


* Code that runs inference on a DICOM volume and produces a DICOM report
location: section3\src

* A report.dcm file with a sample report
location: section3\out\out

* Screenshots of your report shown in the OHIF viewer
location: section3\out\out

* 1-2 page Validation Plan
location: this file