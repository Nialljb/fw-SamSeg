# SamSeg

Sequence Adaptive Multimodal SEGmentation (SAMSEG) is a tool to robustly segment dozens of brain structures from head MRI scans without preprocessing. The characteristic property of SAMSEG is that it accepts multi-contrast MRI data without prior assumptions on the specific type of scanner or pulse sequences used. 




## Overview

[Usage](#usage)

[FAQ](#faq)

### Summary


### Cite

**license:**


**url:** <https://gitlab.com/flywheel-io/flywheel-apps/>

**cite:**  
Fast and sequence-adaptive whole-brain segmentation using parametric Bayesian modeling. O. Puonti, J.E. Iglesias, K. Van Leemput. NeuroImage, 143, 235-249, 2016.

### Classification

*Category:* analysis

*Gear Level:*

* [ ] Project
* [x] Subject
* [x] Session
* [ ] Acquisition
* [ ] Analysis

----

### Inputs

* api-key
  * **Name**: api-key
  * **Type**: object
  * **Optional**: true
  * **Classification**: api-key
  * **Description**: Flywheel API key.

### Config

* debug
  * **Name**: debug
  * **Type**: boolean
  * **Description**: Log debug messages
  * **Default**: false

* input
  * **Base**: file
  * **Description**: input file (usually isotropic reconstruction)
  * **Optional**: false

### Outputs
* output
  * **Base**: file
  * **Description**: segmentated file 
  * **Optional**: false

* parcelation
  * **Base**: file
  * **Description**: parcelation file 
  * **Optional**: true

* vol
  * **Base**: file
  * **Description**: volume estimation file (csv)
  * **Optional**: true

* QC
  * **Base**: file
  * **Description**: QC file (csv)
  * **Optional**: true


#### Metadata

No metadata currently created by this gear

### Pre-requisites

- Three dimensional structural image

#### Prerequisite Gear Runs

This gear runs on BIDS-organized data. To have your data BIDS-ified, it is recommended
that you run, in the following order:

1. ***dcm2niix***
    * Level: Any
2. ***file-metadata-importer***
    * Level: Any
3. ***file-classifier***
    * Level: Any

#### Prerequisite

## Usage

This section provides a more detailed description of the gear, including not just WHAT
it does, but HOW it works in flywheel

### Description

This gear is run at either the `Subject` or the `Session` level. It downloads the data
for that subject/session into the `/flwyhweel/v0/work/bids` folder and then runs the
`synthseg` pipeline on it.

After the pipeline is run, the output folder is zipped and saved into the analysis
container.

#### File Specifications

This section contains specifications on any input files that the gear may need

### Workflow

A picture and description of the workflow

```mermaid
  graph LR;
    A[T1w]:::input --> FW;
    FW[FW] --> FMI;
    FMI((file-metadata-importer)):::gear --> FC;
    FC((file-classifier)):::gear --> D2N;
    D2N((dcm2niix)):::gear --> CB;
    CB((curate-bids)):::gear --> CISO;
    CISO((ciso)):::gear --> SS;
    SS((synthseg)):::gear --> ANA;
    ANA[Analysis]:::container;
    
    classDef container fill:#57d,color:#fff
    classDef input fill:#7a9,color:#fff
    classDef gear fill:#659,color:#fff
```

Description of workflow

1. Upload data to container
2. Prepare data by running the following gears:
   1. file metadata importer
   2. file classifier
   3. dcm2niix
   4. MRIQC (optional)
   5. curate bids
3. Select either a subject or a session.
4. Run the ciso gear (Hyperfine triplane aquisitions)
5. Run the synthseg gear
6. Gear places output in Analysis

### Use Cases

## FAQ

[FAQ.md](FAQ.md)

## Contributing

[For more information about how to get started contributing to that gear,
checkout [CONTRIBUTING.md](CONTRIBUTING.md).]
