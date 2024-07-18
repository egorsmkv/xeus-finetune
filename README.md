# `xeus-finetune`

> [!WARNING]  
> Currently, this work is in progress.

This repository contains training code for [the XEUS model][1] for Automatic Speech Recognition (ASR).
This is a fork of https://github.com/pashanitw/xeus-finetune

## Required software

- Python 3.12
- uv

## Install

```shell
uv venv --python 3.12

source .venv/bin/activate

uv pip install 'espnet @ git+https://github.com/wanchichen/espnet.git@ssl'
git lfs install
git clone https://huggingface.co/espnet/XEUS

uv pip install -r requirements.txt

# in development mode
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
