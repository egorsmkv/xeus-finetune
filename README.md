# `xeus-finetune`

> [!WARNING]  
> Currently, this work is in progress.

This repository contains training code for [the XEUS model][1] for Automatic Speech Recognition (ASR).
This is a fork of https://github.com/pashanitw/xeus-finetune

## Required software

- python3.11, python3.11-dev
- build-essential, cmake
- [uv][2]
- git-lfs

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

## Fine-tuning

1. Authenticate with HF

```shell
huggingface-cli login
```

2. Copy a config file, change dataset sections and hparams

```shell
cp configs/hi_hf.yaml configs/uk_hf.yaml
```

3. Start fine-tuning

```shell
accelerate launch finetune.py --config configs/uk_hf.yaml

# if you want to use only one GPU
accelerate launch --num_processes 1 finetune.py --config configs/uk_hf.yaml
```

## Inference

```shell
python inference.py --ckpt_path <checkpoint path> --audio audio.wav

# example
python inference.py --ckpt_path ./step_2000 --audio audio.wav
```

## Evaluation

Run the following command to calculate Word Error Rate:

```shell
python eval.py --ckpt_path <checkpoint path> --dataset <dataset> --name <subset> --split <split>

# example
python eval.py --ckpt_path ./step_2000 --dataset mozilla-foundation/common_voice_17_0 --name uk --split test
```

## Development

Check and format the code:

```shell
ruff check
ruff format
```

## TODO

- [ ] Enable Flash-Attention for training
- [ ] Set a cache_dir for `load_dataset`

[1]: https://www.wavlab.org/activities/2024/xeus/
[2]: https://github.com/astral-sh/uv
