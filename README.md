# Overview

<TODO: complete this with an overview of your project>
This project is about creating a CICD Pipleline for a python flask project with 
* GitHub as Source Code repository
* Azure Piplelines for deploying
* GitHub Actions for QA and Projekt linting. 
Please note that the Delivery Pipeline can also be created using Github Actions. 

## Project Plan
<TODO: Project Plan

* A link to a Trello board for the project
[link to trello](https://trello.com/b/cSvJb3q5/udacity-2023)
* A link to a spreadsheet that includes the original and final project plan>
see excel file [here](/2023_Udacticty%20DevOpsProject_Michael%20Suren.xlsx)
## Instructions

<TODO:  
* Architectural Diagram (Shows how key parts of the system work)>

<TODO:  Instructions for running the Python project.  How could a user with no context run this project without asking you for any help.  Include screenshots with explicit steps to create that work. Be sure to at least include the following screenshots:
### Preparion Steps: 
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

## ToDos 

* Project running on Azure App Service

* Project cloned into Azure Cloud Shell

* Passing tests that are displayed after running the `make all` command from the `Makefile`

* Output of a test run

* Successful deploy of the project in Azure Pipelines.  [Note the official documentation should be referred to and double checked as you setup CI/CD](https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/python-webapp?view=azure-devops).

* Running Azure App Service from Azure Pipelines automatic deployment

* Successful prediction from deployed flask app in Azure Cloud Shell.  [Use this file as a template for the deployed prediction](https://github.com/udacity/nd082-Azure-Cloud-DevOps-Starter-Code/blob/master/C2-AgileDevelopmentwithAzure/project/starter_files/flask-sklearn/make_predict_azure_app.sh).
The output should look similar to this:

```bash
udacity@Azure:~$ ./make_predict_azure_app.sh
Port: 443
{"prediction":[20.35373177134412]}
```

* Output of streamed log files from deployed application

> 

## Enhancements

<TODO: A short description of how to improve the project in the future>

## Demo 

<TODO: Add link Screencast on YouTube>


