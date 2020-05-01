#################################################################################
# GLOBALS                                                                       #
#################################################################################

PROJECT_DIR := $(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))
PROJECT_NAME = {{ cookiecutter.project_slug }}
PYTHON_INTERPRETER = {{ cookiecutter.python_interpreter }}
VIRTUALENVWRAPPER_PATH:=$(shell which virtualenvwrapper.sh)

ifeq (,$(shell which conda))
HAS_CONDA=False
else
HAS_CONDA=True
endif

## Create virtualenv
environment:
	$(PYTHON_INTERPRETER) -m pip install -U pip setuptools wheel
	export WORKON_HOME={{ cookiecutter.workon_home }}
	mkdir -p $(WORKON_HOME)
	(\
		source $(VIRTUALENVWRAPPER_PATH); \
		mkvirtualenv {{ cookiecutter.virtualenv_name }}; \
	)


requirements:
	(\
		source $(VIRTUALENVWRAPPER_PATH); \
		workon {{ cookiecutter.virtualenv_name }}; \
		pip install -r requirements.txt; \
	)

clean: clean-build clean-pyc ## remove all build, coverage and Python artifacts

clean-build: ## remove build artifacts
	rm -fr build/
	rm -fr dist/
	rm -fr .eggs/
	find . -name '*.egg-info' -exec rm -fr {} +
	find . -name '*.egg' -exec rm -f {} +

clean-pyc: ## remove Python file artifacts
	find . -name '*.pyc' -exec rm -f {} +
	find . -name '*.pyo' -exec rm -f {} +
	find . -name '*~' -exec rm -f {} +
	find . -name '__pycache__' -exec rm -fr {} +


lint: ## check style with flake8
	flake8 {{ cookiecutter.project_slug }}
