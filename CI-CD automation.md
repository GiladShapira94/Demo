# CI/CD Automation Using - Git, Zip, Tar source 

#### Project YAML
Project YAML allows users to define thier project metadata and use this defention when they [load_project()](https://docs.mlrun.org/en/latest/api/mlrun.projects.html#mlrun.projects.load_project) or create [new_project()](https://docs.mlrun.org/en/latest/api/mlrun.projects.html#mlrun.projects.new_project)
In the Project YAML you can define:
* Functions 
* Workflow
* Artifacts
* Source 
On project creation MLRun create a light project YAML, for example: 
````
kind: project
metadata:
  name: default
  created: '2022-06-30T09:41:05.612000'
spec:
  functions: []
  workflows: []
  artifacts: []
  desired_state: online
status:
  state: online
````
For update project YAML use projec.save()

On this section we will cover how to define each topic from the list above and provide an end to end example.

#### Functions
For functions definations use the [set_function](https://docs.mlrun.org/en/latest/api/mlrun.projects.html?highlight=set_function#mlrun.projects.MlrunProject.set_function) method.
* **Parameters  -**
  * func – function object or spec/code url, None refers to current Notebook
  * name – name of the function (under the project)
  * kind – runtime kind e.g. job, nuclio, spark, dask, mpijob default: job
  * image – docker image to be used, can also be specified in the function object/yaml
  * handler – default function handler to invoke (can only be set with .py/.ipynb files), can contain a relative path to the function handler e.g training.model-training (handler model-training in training.py file)
  * with_repo – add (clone) the current repo to the build source
  * requirements – list of python packages or pip requirements file path
