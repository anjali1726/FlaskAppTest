# FlaskAppUTest

- Unittesting project for Python Rest API Flask based

- This project is using Python 3.6.9, which may sometimes be an issue while using latest OS's.
In-case if you are facing issues with the Python version, the GitHub code will work with Python 3.8.0 also.
So you need to install that version with cmd: pyenv install 3.8.0
And, in the jenkins script just replace 3.6.9 with 3.8.0.
pyenv global 3.8.0

## Jenkins CI Pipeline Cmds:

echo "#### Switch to python version 3.8.0 ####"
pyenv versions
pyenv global pypy3.8-7.3.11
python -V

echo "#### Create venv and activate it python version 3.8.0 ####"
python -m venv flaskapp
source flaskapp/bin/activate

echo "##### Install required Python Modules ####"
pip install -r requirements.txt

echo "#### Install Code Coverage Modules ####"
pip install coverage
pip install pytest-cov

echo "####Cobertura - Code Coverage####"
pytest --cov=main --cov-report xml

echo "#### Running Unit Test Cases ####"
pytest utests --junitxml=./xmlReport/output.xml

deactivate
pyenv global system
python -V
