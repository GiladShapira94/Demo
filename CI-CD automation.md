# CI/CD Automation Using - Git, Zip, Tar source 

### Project YAML
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

### Functions
For functions definations use the [set_function](https://docs.mlrun.org/en/latest/api/mlrun.projects.html?highlight=set_function#mlrun.projects.MlrunProject.set_function) method.

Before you creating fucntion YAML you need to the create a fucntion object you can do it with [code_to_function()](https://docs.mlrun.org/en/latest/api/mlrun.html?highlight=code_to_function#mlrun.code_to_function), [new_function()](https://docs.mlrun.org/en/latest/api/mlrun.run.html?highlight=new_function#mlrun.run.new_function).
After you creating a function object you can use the [export()](https://docs.mlrun.org/en/latest/api/mlrun.runtimes.html?highlight=export#mlrun.runtimes.BaseRuntime.export) method, For Example:
````
<function object>.export('./model_training.yaml')
````

The set_function method allow you to set the functions attributes in the project YAML, for example: 
function source (YAML, py, ipynb, function object) , name of the fucntion, function handler, function image and kind

**Important Note -** Remote functions as Serving and Nuclio need to set with thier function object to function YAML
````
project.set_function(
    name="training", handler="training.model_training",
    image="mlrun/mlrun", kind="job", with_repo=True,
)
````
Or
````
project.set_function(
    func="training.yaml")
````
### Artifacts

