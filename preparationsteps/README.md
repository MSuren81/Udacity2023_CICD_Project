# Udacity2023_CICD_Project
udactity2023 CICD Pipeline project

# Setup the Azure Cloud Shell and the Connection
- setup Github
- Integrate Azure 
- Setup Scaffolding

## Generate the SSH-Key in AZure Cli
Open the Azure CLI and enter the following command
``` az
ssh-keygen -t rsa
```

After Creating the key use this command
`cat` and the location of the public key to print the key. 
Add this key to github under Settings, your profile, 

See this screenshot for the established connection: 
![alt text](/images/2023-04-04 20_26_54-Azure-Github-Connection.png"Connecting Azure and GitHub")

## Project Scaffolding
* Create a Make file
``` makefile
install:
	pip install --upgrade pip &&\
		pip install -r requirements.txt

test:
	python -m pytest -vv test_hello.py


lint:
	pylint --disable=R,C hello.py

all: install lint test
```
* Create a requirements.txt file
``` txt
pylint
pytest
```

## Create a virtual environment for python in AZ
`python3 -m venv ~/.Udacity-CICD-Project`
`source ~/.Udacity-CICD-Project/bin/activate`

## Create a script and testfile for python
Create the file `hello.py`
``` python
def toyou(x):
    return "hi %s" % x


def add(x):
    return x + 1


def subtract(x):
    return x - 1
```
and create the test file `test_hello.py`
``` python
from hello import toyou, add, subtract


def setup_function(function):
    print("Running Setup: %s" % function.__name__)
    function.x = 10


def teardown_function(function):
    print("Running Teardown: %s" % function.__name__)
    del function.x


### Run to see failed test
#def test_hello_add():
#    assert add(test_hello_add.x) == 12

def test_hello_subtract():
    assert subtract(test_hello_subtract.x) == 9
```

## run make all in the virtual environment
run `make all` on your local virtual environment. 
See this screenshot for the result:
![Alt text](/images/2023-04-04%2021_13_51-make-all-on-local.png "Make all on local")


## added github action for testing
``` yml
name: Python application test with Github Actions

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up Python 3.11
      uses: actions/setup-python@v1
      with:
        python-version: 3.11
    - name: Install dependencies
      run: |
        make install
    - name: Lint with pylint
      run: |
        make lint
    - name: Test with pytest
      run: |
        make test
```
The actions will be executed after a push to the branch. 
Please note that you adjust your python version in the yml file above
This Image will show the results after the run. 

![Alt text](/images/2023-04-04%2023_05_39-Actions-executed.png "GitHub Action executed")
![Alt text](/images/2023-04-04%2023_03_36-Github-Actionbuild-test.png "Pylint and test")

``` bash

BGROUP+SURE001@ASY-7837482163 MINGW64 /c/_git/Udacity2023_CICD_Project (main)
$ python -m venv c:/_git/Udacity2023_CICD_Project/.venv/

BGROUP+SURE001@ASY-7837482163 MINGW64 /c/_git/Udacity2023_CICD_Project (main)
$  source c:/_git/Udacity2023_CICD_Project/.venv/Scripts/activate
(.venv) 
```