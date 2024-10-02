# Neuroscience Lab - fMRI Analysis  
**Due Date**: 15th Khordad, 1403 (June 2024)  
---



## Data Required
- **Functional slice timing data**: (server -> neuro? -> hw)
- **Structural and functional data**: (server -> neuro? -> hw)
- **Task timing information**: (CW)

---

## Tasks

### 1. **Structural Data Processing**  
   a) **Skull Stripping**: Remove the skull and surrounding areas from the structural data. Overlay the obtained volume onto the initial image and extract three main AFNI slices from the brain in this condition.  
   
   b) **Volume Estimation**: Estimate the volume captured by the MRI device from the structural data.  
   
   c) **Grey Matter Mask**: Overlay the skull-stripped image onto the original structural image. Click on various areas of the brain to approximate the grey matter and white matter values. Using the `3dCalc` function, create a grey matter mask by setting a suitable value range (e.g., between 1500 to 2500) for the grey matter (yellow spectrum), white matter (red spectrum), and ventricles (blue spectrum).  

---

### 2. **Functional Data Preprocessing**  
   a) **Preprocessing Pipeline**: Preprocess the functional data according to the discussed pipeline.

   b) **Slice Timing vs Motion Correction**: Analyze the difference in preprocessing error when applying slice timing correction before or after motion correction. Use `3dinfo` and `3dTshift` commands for this task. (Note: The step for removing initial volumes has already been performed.)

---

### 3. **Alignment of Functional and Structural Images**  
Align the functional data with the structural data, as discussed in class. Save the reverse transformation (from functional to structural) for future use.

---

### 4. **Regressor Creation**  
The experiment involves detecting either a typical or atypical stimulus. Each trial includes a short, 200ms bright spot. Typical stimuli are small green spots, while atypical stimuli are larger red spots. The subject presses a button to report detection of atypical stimuli.

   - Create regressors for the three events: typical flash, atypical flash, and button press. For the button press event, use the reaction time (RT) as the duration, subtracting 200ms from the recorded RT to account for the offset between stimulus and response. Refer to the `3dDeconvolve` documentation for building the regressors.

---

### 5. **GLM Analysis**  
Use `3dDeconvolve` to perform General Linear Model (GLM) analysis. Explain whether using this command at this stage is appropriate and if the current GLM output is useful. Continue using this GLM output for further analysis in the report.

---

### 6. **Mapping GLM Coefficients to Structural Images**  
Use `3dAllineate` to align the GLM beta maps with the structural images. Display each regressor’s beta map and the contrast map (oddball vs. standard) in AFNI, applying a threshold of **p = 0.05** to preserve only statistically significant activations.  
   - For each beta map, click on areas with the highest activation, and provide orthogonal slice views for each of the 4 beta maps (12 images in total).

---

### 7. **Correcting Activity Maps for False Positives**  
   a) **Noise Correlation Calculation**: Align the GLM residuals with the structural image, then calculate spatial noise correlation parameters using the `3dfwhmx` command and the grey matter mask from Task 1. Compare the calculated FWHM with those used during preprocessing.  
   
   b) **Cluster Size Calculation**: Use `3dClustSim` to compute the minimum cluster size for **p = 0.01** and **p = 0.05** under the condition that the false positive rate remains below **0.05**. Include tables generated by `3dClustSim` for **NN = 1** in the report.

   c) **Revised Activity Maps**: Create new beta maps similar to Task 6, applying the cluster size threshold from Task 7b. Include images of the three largest clusters and attach the RPT table from AFNI.

---

## References
- Ghazizadeh, A., Griggs, W., & Hikosaka, O. (2016). Object-finding skill created by repeated reward experience. *Journal of Vision*, 16(10):17, 1–13. DOI: [10.1167/16.10.17](https://doi.org/10.1167/16.10.17)