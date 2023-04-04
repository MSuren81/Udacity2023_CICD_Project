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
![alt text](https://github.com/MSuren81/Udacity2023_CICD_Project/blob/9168a32bf7ecc49d5baaf4cd1d08126b8ae43bd4/images/2023-04-04%2020_26_54-Azure-Github-Connection.png "Connecting Azure and GitHub")

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
