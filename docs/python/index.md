---
title: Python
date: 2022-01-01
tags:
    - 'python'
    - 'setup'
---


## Python environment
Suggest to use virtual python which will not making your system python messup 
```shell title="Shell"
# Mac OS 

## if no pyenv installed, run:
brew install pyenv

## install python by pyenv
pyenv install 3.10.2

## Create python-virtual-environments
pyenv global system 3.10.2
python3.10 -m venv env

## active your virtual environment
source env/bin/activate

## !To stop using that environment, you just need to deactivate 
deactivate
```

## Install requirement python package

Install requirement package inside virtual environment
`pip install -r requirements.txt`


## upgrade package by pip & requirement file

`pip install --upgrade --force-reinstall -r requirements.txt`


## iterate over files and print line with keyword

```
# import required module
import os
 
# assign directory
directory = '.'
 
# assign keyword
keyword = "args['log_hash']:"

# iterate over files and print line with keyword
for filename in os.scandir(directory):
    if filename.is_file():
        # print(filename.path)
        with open(filename.path, 'r') as f:
            data = f.readlines()
            for line in data:
                if keyword in line:
                    print(line)
```