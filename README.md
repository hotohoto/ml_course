# Introduction to python and machine learning

## How to setup

```bash

# install prerequisite system libraries for scipy(?)
sudo apt install libblas3 liblapack3 liblapack-dev libblas-dev gfortran

# setup python environment
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Install pytorch following https://pytorch.org/get-started/locally/
pip install torch==1.7.1+cpu torchvision==0.8.2+cpu torchaudio==0.7.2 -f https://download.pytorch.org/whl/torch_stable.html
```
