# swe-bench-docker
Create, customize, and manage SWE-Bench containers


## Prepare environement:

```bash
python3.10 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
pip install -e ./SWE-bench
```

## Usage
```bash
usage: execute_in_docker.py [-h] instance_id test_paths files_to_copy test_folders

positional arguments:
  instance_id    Instance id of and issue, e.g, django__django-14752
  test_paths     A file containing pairs of (test file paths or names on the host machine, paths/names inside the docker)
  files_to_copy  A file containing the list of all files that should be copied from the host machine to the docker container (including generated test files)
  test_folders   A file containing pairs of (project name, deault parent test folder, e.g, 'django /testbed/tests')

options:
  -h, --help     show this help message and exit
```

### Structure of files_to_copy file
One pair per line. The pair is separated by '#'.
The two first lines should always be present, but, do not forget to replace "pytest-dev__pytest-7432" with the actual issue_id you are working on.
```txt
build_files/pytest-dev__pytest-7432/eval.sh#/testbed/eval.sh
build_files/pytest-dev__pytest-7432/patch.diff#/testbed/patch.diff
PATH/TO/SOME/FILE/ON/YOUR/MACHINE#DESTINATION/PATH/ON/DOCKER/CONTAINER
...#...
...#...
```

### Structure of test paths
```
PATH/TO/GENERATED/TEST/FILE#DESTINATION/PATH/ON/DOCKER
...#...
```
The destionation path should not include the prefix path which is found in test_folders file (respect this rule especially for django).

Example files are given: test_folders, test_paths, and files_to_copy

## Next improvements:
https://github.com/islem-esi/swe-bench-docker/issues/2

https://github.com/islem-esi/swe-bench-docker/issues/1

If there are other issues or needed improvements, please raise an issue and assign a label accordingly...