# Retinal Blood Vessel (RBV) Segmentation

## Problem

Manual analysis of fundus images to detect retinal blood vessels (RBV) is time-consuming, requires expertise, and prone to variability. Automated methods ensure consistent performance and can handle multiple datasets without human bias. While deep learning (DL) methods perform well, they require large annotated datasets and high computational resources. Traditional filter-based approaches are faster and less data-hungry but often struggle with smaller vessel detection.

## RBV Overview

*(Insert pipeline diagram here, showing preprocessing → B-COSFIRE → Frangi → Postprocessing → Final Output)*

## Approach

### Preprocessing

* Extract the green channel from the RGB fundus image and apply CLAHE for contrast enhancement.
  *(Insert image: preprocessed green channel + CLAHE)*
* Generate ROI mask from the original RGB image by converting to CIE Lab, using the L channel, and applying isodata thresholding. Only white regions in the ROI are processed; black regions are ignored.
  *(Insert image: ROI mask)*

### Feature Extraction – B-COSFIRE

* Apply B-COSFIRE filter (Bar Combination of Shifted Filter Responses) to the preprocessed image within the ROI.
* Combines symmetric and asymmetric filter responses to enhance vessel structures.
* Captures larger vessels, but smaller vessels may need additional enhancement.
  *(Insert image: B-COSFIRE output)*
* [Reference: Azzopardi et al., 2015, *B-COSFIRE: A trainable filter for line pattern recognition*]

### Feature Extraction – Frangi

* Apply Frangi filter on the inverted B-COSFIRE output.
* Enhances smaller vessel structures using eigenvalues of the Hessian matrix.
* Parameters (alpha, beta, gamma, scale) tuned based on B-COSFIRE settings.
  *(Insert image: Frangi output)*

### Postprocessing

* Combine outputs from B-COSFIRE and Frangi filters.
* Binarize the image and remove noise/artifacts to obtain the final vessel map.
  *(Insert image: Final vessel segmentation overlay)*

## Results

| Dataset | Sensitivity | Specificity | Accuracy |
| ------- | ----------- | ----------- | -------- |
| DRIVE   | —           | —           | —        |
| STARE   | —           | —           | —        |
| HRF     | —           | —           | —        |

*The proposed method achieves a good balance of sensitivity and specificity while improving true vessel detection, comparable to deep learning approaches and higher than most past non-DL methods.*

## Visuals

* All images referenced above are to be inserted inline where mentioned. No source code or implementation details are included, only the methodology and outputs for portfolio presentation.
