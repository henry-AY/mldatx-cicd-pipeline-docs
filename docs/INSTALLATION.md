# Installation Guide

This guide describes how to install and configure the environment required to run automated Simulink Test execution from Python using the scripts in this repository. The setup supports local execution as well as CI/CD workflows.

</hr>

## Prerequisites

Before you begin, ensure you have the following installed:

### 1. MATLAB Requirements
* MATLAB (R2023b or later recommended)
* Simulink + Simulink Test

Matlab must be accessible from the command line via the `matlab` executable.

To test this:

```bash
matlab -h
```

If MATLAB is not found, add it to your system PATH.

</hr>

### 2. Python Requirements 
* Python 3.8+
* Recommended: a virtual environment

You will also need the following Python packages:
```bash
pip install -r requirements.txt
```

</hr>

### 3. Operating System Compatibility (verified + tested)
* MacOS
* Ubuntu

</hr>

### Repository Structure
A typical layout looks as such:

```arduino
matlab-root/
│
├── cicd-scripts/
│   └── ...
│
├── projects/
│   └── <subsystem-name>/
│       ├── tests/
│       ├── results/
│       └── models/
│
└── other files
```

Your repo may slightly vary; however, this structure is essential for the pathing of the program. The automation expects:
* A `tests/` folder containing .mldatx test suites
* A `results/` folder where test results can be exported
* A JSON configuration file defining folder structure

</hr>

### Running Tests Locally

The repository can be run by navigating to the `matlab-root` and running the following command.

```bash
python cicd-scripts/parent.py
```

This script will:
* Pull files from the correct repository
* Launch MATLAB in batch mode
* Run the latest test suite (`.mldatx`)
* Export results to the `results/` folder
* Return a machine-readable exit code
* Final results + message is exported to a CSV.

Logs are written to the `logs/` directory.

</hr> 

### Log Files

Log files are stored in:

```bash
logs/run_YYYY-MM-DD.log
```

This folder & file are automatically created.

</hr>

### Support

If you encounter issues:
1. Open a GitHub Issue
2. Include:
  * The log file (`scripts-logs/run_*.log`)
  * MATLAB Version
  * Python Version
