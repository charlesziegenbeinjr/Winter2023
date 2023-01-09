# Functional Magnetic Resonance Imaging Methods
- Is a paper concerned with giving an overview of what fMRI is

## Introduction
- All fMRI rely on BOLD - blood oxygenation level dependent - changes in brain tissue
    - Up/Down regulated metabolic activity caused by cognitive tasks
    - Magnetic Resonance comes from the magnetic properties of hemoglobin, changes in states
- Two primary types of fMRI study:
    1. Cognitive tasks used to modulate specific neuronal activity
    1. Resting state studies
    - Time series in nature, watch the brain change in every voxel
- Driving Point: review methods employed to acquire and process BOLD fMRI data, draw inference on neural properties

## fMRI Experiments

### Task-Based Study
- Compare observation of brain activity with a hypothesized model, voxel in the brain is a 3D block of tissue
    - Find the areas that respond, test them further against more rigid models
        - Genotypical, phenotypical, difficulty of task
___
Does this work? Seems that this varies from person-to-person with regards to genotype?
___
- Experimental and control groups have scans taken over time, still hard to estimate what BOLD contrast changes will happen
___
What is the linear assumption for BOLD contrast?
___
- Task designs: block trial and event-related trial
    - Block trial is best for detecting activation
    - ER Trial is bestg for characterizing time course of activation
        - Mixed designs in between, but no mention of their effectiveness
- Noise is present from different portions, can be from cardiac activity, medication, etc.
    - Dealt with via pre-processing

### Resting-State fMRI
- Hypothesis is that distinct brain regions fluctuate
    - Collect extraneous data to avoid noise, calibrate this with the readings collected


## Acquiring Data
- Single-shot acquisitions, interleaved (1,3,5/2,4,6)

## Analysis

### Pre-Processing
- Variations due to head motion, magnetic field problems, etc.
    - Can change the patterns displayed, reduce detection power of statistical analysis, alter conclusions
- Pre-processing pipeline established
___
What are the "statistical analyses" that are conducted
___
#### Quality Assurance
- Effectively looking at the data post-scan to determine its usability
    - Is this subjective? Is there a standard method to determining which data is the best?

#### Slice Timing Correction
- Temporal issues when slices are one at a time over a period of time, can lead to incorrect causal relationships
- Fix with temporal interpolation, estimates the signal amplitude for each slice/voxel at reference time by interpolating from neighboring TR
___
How accurate is the interpolation? What are the adverse effects of this kind of estimation?
___

#### Head Motion Correction
- Participant head motion can throw off results
- Can prevent with fixation, have the head secured in a particular area, spatial interpolation, temporal interpolation to suppress motion artifacts
- Can fix at runtime with prospective motion correction, utilizes head position information to follow as scan progresses

#### Distortion Correction
- Magnetic field non-uniformity, can cause results to be distorted
- Correct with hardware compensation. measure the field heterogenity and interpolate

#### Temporal Filtering
- Eliminate noisy frequencies and preserves signal frequency

#### Spatial Smoothing
- Improve fSNR of data, suppress noise sources that are uncorrelated among adjacent imaging voxels
- Mitigate the difference between the inherent spatial structure and assumed model
- Ameliorate the variations between subjects

#### Physiological Noise Correction
- Fluctuations due to bodily processes
- Cyclic in nature, can be resolved and filtered out of the data
    - Model the noise via external recording, or estimate from the data itself

#### Functional-Structural Co-Registration
- Resample anatomical data and transform
___
What cost function is minimized?
___

#### Spatial Normalization
- Can the normalization of a person's brain incur some bias? 
- The authors discuss whether normalization should be done before or after statistical analysis, but do not comment on when the normalization is applicable.
- Global signal regression can introduce the ability to infer neural activity
    - Recommendations against, situations for using it provided

### Analysis of Task Studies
- Experimental vs control, test whether experimental hypothesis $\not =$ to control hypothesis, null hypothesis being opposite

#### T Testing
- Each time point as independent sample, compare amplitudes using two-sample student's t test
- Voxels might not activate immediately, this must be taken into consideration
- Rarely used

#### Correlation Analysis
- Examine temporal synchrony between voxel's time series  and predicted response of the experiment
- Apply t-test, use correlation between voxels
- Only possible when testing a single hypothesis

#### General Linear Model Analysis
- Examine experimental and predicted results
- Linear mixture of several model factors, added noise
- Factors and parameter weights
- GLM predicts how well each voxel's time series is fit by linear combination of model factors
    - F-statistics
- Test stat significance of param weight

#### Multi-Variate Pattern Analysis
- MPVA toolboxes
- 3 reasons why it is hard to use

#### Correction for Multiple Comparisons
- How to determine false-positives
    - Different ways to do this, assigning new error criterias

#### Inter-Subject Analysis
- Biodiversity, combone results across subjects to test experimental hypothesis
    - Combine time points, fixed-effect analysis

### Advanced Analysis
- Functional and effective conmnectivity
    - what kind of effect does one neuronal system have on the other
- Assumptions of the inherent ddata structure or biophysics
- 