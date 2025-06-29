# React-QC
This is an open source project that is contributing a paper to PRCV, titled: Joint Artifact Correction and Quality Assessment via
Perceptual Contrastive Learning on Diffusion MRI

## Introduction
Framework for Joint Artifact Correction and Quality Assessment in dMRI: This work tackles artifacts (ghosting, motion) impairing dMRI microstructure analysis. We propose a novel two-stage framework:
* **Artifact Correction**: Utilizes an enhanced 3D U-Net with Leaky ReLU and trilinear upsampling, trained using a hybrid perceptual loss (NMAE + HaarPSI) for high-fidelity artifact removal across 4D DWI.
* **No-Reference Quality Assessment**: Generates a pseudo-reference by comparing low-level (MSE) and high-level perceptual (LPIPS, HaarPSI) features before/after correction, enabling accurate artifact classification via SVM. The framework demonstrates superior robustness across acquisition protocols and outperforms existing methods, offering a reliable technical foundation for automated dMRI quality control.


## Key elements covered across these options
> * **Problem**: Artifacts (ghosting, motion) in dMRI hinder analysis.
> * **Solution Core**: Joint artifact correction & quality assessment.
> * **Key Innovation 1**: Enhanced 3D U-Net for correction with hybrid perceptual loss.
> * **Key Innovation 2**: Pseudo-reference NR-IQA using correction-derived features & SVM.
> * **Key Benefit**: Robustness across protocols & superior performance vs. other methods.
> * **End Goal**: Reliable automated quality control for clinical dMRI.

## Project Structure
```
|—— dataset.py                 # Dataloader for training, validation, and testing
|—— model.py                   # Model architecture for improved 3D Unet training
|—— train.py                   # Training React-QA code
|—— test_model_generate_npy.py # Using trained model to generate npy files which contains MSE, LPIPS, and HaarPSI features
|—— haarpsi.py                 # Calculate HaarPSI index which indicates the similarity between two images
|—— classify_code.py           # Using SVM to classify the quality of the image which generated by test_model_generate_npy.py
|—— npy_file/                  # Numpy files for storing MSE, LPIPS, and HaarPSI features that are generated by test_model_generate_npy.py
|   └── train
|   └── val
|—— requirements.txt           # Requirements that are needed to run the project
```

## Usage
To use this project, follow these steps:
1. Install the required packages by running `pip install -r requirements.txt`.
2. Then you can run `python train.py` to train the model, you need to choose the best model.
3. Using step 2 model to generate npy files by running `python test_model_generate_npy.py`
that you can save npy files in npy_file/train or npy_file/val
4. Finally you can run `python classify_code.py` to classify the quality of the volume exclude b0 from DWI images
