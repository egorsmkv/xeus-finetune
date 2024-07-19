# `xeus-finetune`

> [!WARNING]  
> Currently, this work is in progress.

This repository contains training code for [the XEUS model][1] for Automatic Speech Recognition (ASR).
This is a fork of https://github.com/pashanitw/xeus-finetune

## Required software

- python3.11, python3.11-dev
- cmake
- uv
- git lfs

> [!NOTE]  
> Python 3.12 cannot be used because one of the dependencies in ESPnet relies on an old package.

## Install

```shell
uv venv --python 3.11

source .venv/bin/activate

# install espnet
git clone --branch ssl --depth 1 https://github.com/wanchichen/espnet espnet-code
cd espnet-code
git fetch --unshallow
uv pip install -e .

# download XEUS checkpoint
git clone https://huggingface.co/espnet/XEUS

# install required packages
uv pip install -r requirements.txt

# in development mode install additional packages
uv pip install -r requirements-dev.txt
```

## Development

Check and format the code:

```shell
ruff check
ruff format
```

## TODO

- [ ] Enable Flash-Attention for training

[1]: https://www.wavlab.org/activities/2024/xeus/
