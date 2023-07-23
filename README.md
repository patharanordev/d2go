# d2go on Window11

## Requirement

- Python 3.8
- CUDA 12.2
- Windows 11
- Anaconda 3 (***Optional***)

## Preparation

You need to know first, your environment ready for GPU usage.

Let's start from installing the correct `torch` version (Ref. https://pytorch.org/get-started/locally/) which match with current CUDA version on your Windows, in this case it is `12.2` :

```sh
pip install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu121
```

Checking `torch` with CUDA available or not :

```sh
python -c 'import torch;import torchvision; print(torch.cuda.is_available())'
```

## Installation

> ---
>
> [***Optional***] Install python kernel module to support Jupyter notebook :
>
> ```sh
> pip install ipykernel
> ```
>
> Create the kernel with python 3.8 :
>
> ```sh
> python -m ipykernel install --user --name py38gpu
> ```
>
> ---

Create environment for anaconda :

```sh
conda create -n d2go python=3.8.0
conda activate d2go
```

Install `torch`:

```sh
pip install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu121
```

Install `detectron2`'s dependencies :

```sh
python -m pip install 'git+https://github.com/facebookresearch/detectron2.git'
```

> ---
> If you got error like this :
>
> ```sh
> ...
> 
>       3 errors detected in the compilation of "C:/Users/patha/AppData/Local/Temp/pip-req-build-7pdw3whx/detectron2/layers/csrc/nms_rotated/nms_rotated_cuda.cu".
>       nms_rotated_cuda.cu
>       error: command 'C:\\Program Files\\NVIDIA GPU Computing Toolkit\\CUDA\\v12.2\\bin\\nvcc.exe' failed with exit code 2
>       [end of output]
> 
>   note: This error originates from a subprocess, and is likely not a problem with pip.
>   ERROR: Failed building wheel for detectron2
>   Running setup.py clean for detectron2
> Failed to build detectron2
> ERROR: Could not build wheels for detectron2, which is required to install pyproject.toml-based projects
> ```
>
> Please clone the repository :
>
> ```sh
> git clone https://github.com/facebookresearch/detectron2 detectron2_repo
> ```
>
> and set `FORCE_CUDA="1"` in your terminal (ex. PowerShell):
>
> ```ps1
> set FORCE_CUDA="1"
> ```
>
> Then install the dependencies manually (it requires `ninja` to build package) :
>
> ```sh
> pip install ninja
> pip install -e ./detectron2_repo
> ```
>
> ---

Install `mobile_cv` :

```sh
python -m pip install 'git+https://github.com/facebookresearch/mobile-vision.git'
```

Then `d2go` :

```sh
git clone https://github.com/facebookresearch/d2go d2go_repo
pip install -e ./d2go_repo
```

## Usage

Ref. [notebook]()

## Other Issues

### Docker : WSL2 got low memory usage

Please try to update your `C:\Users\<YOUR_USER_NAME>\.wslconfig` :

```txt
# Settings apply across all Linux distros running on WSL 2
[wsl2]

# Limits VM memory to use no more than 4 GB, this can be set as whole numbers using GB or MB
memory=8GB 

# Sets the VM to use two virtual processors
processors=2

# Sets amount of swap storage space to 8GB, default is 25% of available RAM
swap=8GB

# Turn off default connection to bind WSL 2 localhost to Windows localhost
localhostforwarding=true

# Turns on output console showing contents of dmesg when opening a WSL 2 distro for debugging
debugConsole=true
```
