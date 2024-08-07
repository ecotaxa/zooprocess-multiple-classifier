# zooprocess-multiple-classifier
[![Build Status](https://jenkins.services.ai4os.eu/buildStatus/icon?job=AI4OS-hub/zooprocess-multiple-classifier/main)](https://jenkins.services.ai4os.eu/job/AI4OS-hub/job/zooprocess-multiple-classifier/job/main/)

A module to differentiate images containing multiple zooplankton objects from those containing only only one object.

It processes regions of interest (ROIs or 'vignettes') extracted by ZooProcess from an original image taken by the ZooScan instrument.

These ROIs should contains only one object for later classification. This module tries to predict which image contain multiple objects so that they can then be separated before their classification. The separation is done by another module called ai4os-zooprocess_multiple_separator.

This application uses a MobileNet v3 classifier trained towards maximizing the recall of the 'multiple' class. It returns the predicted class and associated probability.

To launch it, first install the package then run [deepaas](https://github.com/ai4os/DEEPaaS):

```bash
git clone https://github.com/ai4os-hub/zooprocess-multiple-classifier
cd zooprocess-multiple-classifier
pip install -e .
deepaas-run --listen-ip 0.0.0.0
```

## Project structure

```
│
├── Dockerfile             <- Describes main steps on integration of DEEPaaS API and
│                             zooprocess_multiple_classifier application in one Docker image
│
├── Jenkinsfile            <- Describes basic Jenkins CI/CD pipeline (see .sqa/)
│
├── LICENSE                <- License file
│
├── README.md              <- The top-level README for developers using this project.
│
├── VERSION                <- zooprocess_multiple_classifier version file
│
├── .sqa/                  <- CI/CD configuration files
│
├── zooprocess_multiple_classifier    <- Source code for use in this project.
│   │
│   ├── __init__.py        <- Makes zooprocess_multiple_classifier a Python module
│   │
│   ├── api.py             <- Main script for the integration with DEEPaaS API
│   |
│   ├── config.py          <- Configuration file to define Constants used across zooprocess_multiple_classifier
│   │
│   └── misc.py            <- Misc functions that were helpful accross projects
│   │
│   └── utils.py           <- Contains the actual code to perform inference
│
├── data/                  <- Folder to store the data
│
├── models/                <- Folder to store models
│   
├── tests/                 <- Scripts to perfrom code testing
|
├── metadata.json          <- Metadata information propagated to the AI4OS Hub
│
├── pyproject.toml         <- a configuration file used by packaging tools, so zooprocess_multiple_classifier
│                             can be imported or installed with  `pip install -e .`                             
│
├── requirements.txt       <- The requirements file for reproducing the analysis environment, i.e.
│                             contains a list of packages needed to make zooprocess_multiple_classifier work
│
├── requirements-test.txt  <- The requirements file for running code tests (see tests/ directory)
│
└── tox.ini                <- Configuration file for the tox tool used for testing (see .sqa/)
```
