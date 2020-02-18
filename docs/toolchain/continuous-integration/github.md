# GitHub

## GibHub Action

Example: `.github/workflows/docs-update-check.yml`

```yml
name: Docs Update Check

on:
  push:
    branches:
    - master
  schedule:
    - cron: "0 8 * * *"

jobs:
  updchck:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v1
    - name: Set up Python 3.8
      uses: actions/setup-python@v1
      with:
        python-version: 3.8
    - name: Set up Cache
      uses: actions/cache@v1
      with:
        path: ~/.cache/pip
        key: ${{ runner.os }}-pip-${{ hashFiles('**/Pipfile.lock') }}
        restore-keys: |
          ${{ runner.os }}-pip-
    - name: Install Pipenv
      run: pip install pipenv
    - name: Install Dependencies
      run: pipenv install
    - name: Check Docs Source Update
      run: pipenv run updchck
```
