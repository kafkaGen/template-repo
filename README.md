# Template repository for ML projects

This repository is a template for machine learning projects. It is designed to be a starting point for new projects, providing a basic structure and a set of tools to help you get started.

## Getting started
1. Clone the repository
2. Install Poetry package manager
3. Install the project dependencies:
```bash
poetry config virtualenvs.in-project true && poetry install
```
4. Install pre-commit hooks:
```bash
poetry run pre-commit install
poetry run pre-commit autoupdate
```
5. Install types for mypy:
```bash
poetry run mypy --install-types --non-interactive
```
6. Develop your project
7. Export the environment:
```bash
poetry export --without-hashes --format=requirements.txt > requirements.txt
```

## Git Branches Strategy:
- `main` branch used for production version, has own prod environment
- `hotfix` branch, clone from `main`, to add quick minor fixes to prod version (need to be sure, that changes are not essential!), merged to `main`
- `develop` branch used for continuous updating project with new functionality and testing, after completing some release, merged to `main`, has own dev environment
- `feature_<name>` branch to develop new feature, clone from `develop`, after finishing, merged to `develop`

## Single Microservice Strategy

### Project structure:
```
.
├── .git
├── .github				        # ci/cd
├── .hydra_logs			        # microservice run logging folder
├── <microservice-name>		    # source file of microservice
|	├── <python-module>
|	├── utils.py
|	└── main.py
├── <gitsubmodule_name>		    # git submodules in case of code share from other projects
├── config				        # hydra config storage folder
├── datasets
├── docker
|	├── Dockerfile
|	└── docker-compose.yaml
├── test
├── train
├── weights
├── .env.dev				    # Dev env for docker compose
├── .env.prod			        # Prod env for docker compose
├── .gitignore
├── .gitmodules
├── .pre-commit-config.yaml
├── README.md			        # Documentation about the project, "How-to" for deployment and description of main complex components
├── pyproject.toml			    # package configurations
└── requirements.txt
```   

### Tools:
- Python 3.11 \
Currently the most stable version of Python, brings speed and efficiency optimization, match operator (in earlier version), better interpreter error hinting. Python 3.12 is incompatible with kafka and torchvision packages by 26 Apr 2024.
- Docker, docker compose \
In docker-compose.yaml you can use ${ENV_VARIABLE} that is read from a .env file, in such a way you can use the same docker-compose.yaml file with different .env files for different environments. 
- Hydra \
Useful tool to store all project configuration files in one place, allowing you to change configuration on the fly. Easy usage of ENV VARIABLE in config.
- Pydantic, Enum \
Efficient way to create and use custom data structure with input validation.
- Poetry, conda, venv \
Poetry very useful Python package manager and package builder, highly customizable, support dev package list. Alternatively use casual Conda or Python virtual venv.
- .pre-commit hooks \
Cool feature that runs some customizable checks on your code before you make a git commit, preventing you from delivering unformatted code, large files, sensitive data, etc. Best place to integrate them is in CI when pushing to the main or develop branch.
- cProfile, scalene \
cProfile - common tool to profile your Python code for CPU and RAM usage to find bottlenecks, do not support parallel computing and GPU. Scalene - more powerful tools, brings profiling for CPU, RAM, GPU, support asynchronous and parallel processing.

