# config_stp_wcc

Space Telescope Pathfinder's WCC-specific repository for support data and configuration management as an installable python package 

Details on the change control process are found in the [coronograph design documentation repository](https://github.com/uasal/spacecoron_design_docs)

The parameters for each subsystem are found in the `configs` directory, and supporting data is found in the `support_data` directory.
A description of how configurations are used in UASAL software, users can find an example notebook in the `docs` directory of the  [config_project_template](https://github.com/uasal/config_project_template) repository. 
## Dependencies and Requirements

config_stp_wcc is dependent on [utils_config](https://github.com/uasal/utils_config) but will automatically be installed via 
```sh 
pip install "git+https://github.com/uasal/utils_config.git@develop"
```

ssh keys are necessary for the pip-based install. Verify you have ssh keys installed in GitHub, or check out this [ssh key tutorial](https://github.com/uasal/lab_documents/blob/main/ssh_key_tutorial.md)

## Pip Installation

```sh
pip install git+ssh://git@github.com/uasal/config_stp_wcc.git
```

## Git Clone Installation

### **1. Clone the Repository**
```sh
git clone git@github.com:uasal/config_stp_wcc.git
cd config_stp_wcc
```

### **2. Install the Package**
```sh
pip install .
```

## Usage

config_stp_wcc makes usage of the ConfigLoader class (as *config_loader*) from utils_config via the `load_config_values` method, accepting 'raw' 'parsed' or 'unitless' as an argument, returning a dictionary after parsing the 'configs' directory for .toml filies
```python
import config_stp_wcc
data = config_stp_wcc.load_config_values()
```

load_config_values() has a default argument of 'raw' but alternatively accepts 3 arguments that trigger data to be formatted differently: 
- `load_config_values('unitless')` -> 0.01
- `load_config_values('parsed')` -> {'value': 0.01, 'unit': 'arcsecond'}
- `load_config_values('raw')` -> 10e-3arcsecond

For importing data and keeping code consistent across installs, config_stp_wcc will return the path to support_data with `get_data_path()`
```python
import config_stp_wcc
data_path = config_stp.get_data_path()
print(data_path)
``` 

## Git large file storage (LFS)

This repository makes use of the git large file storage for files listed in the `.gitattributes` file.
Accessing these files will require users having (Git Large File Storage (LFS))[https://docs.github.com/en/repositories/working-with-files/managing-large-files/installing-git-large-file-storage] installed on their local machine.

If you have Git LFS installed, then the large files will be pulled by default.
This can be disabled in your gitconfig, as described (at this link)[https://stackoverflow.com/questions/42019529/how-to-clone-pull-a-git-repository-ignoring-lfs].
