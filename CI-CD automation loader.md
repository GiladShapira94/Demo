# Load project YAML from - Git, Zip, Tar source

After you create your project YAML you can simply load that project and run, build and deploy your function.

In this session you would learn how to:
* get a function object 
* run a function
* build a function
* deploy a function
* run a workflow

#### Get Function Object 
For gets function object you will need to use the [get_function](https://docs.mlrun.org/en/latest/api/mlrun.projects.html?highlight=get_function#mlrun.projects.MlrunProject.get_function) method.
This method allows you to get a function object based on the metadata in your project YAML file,
````
serving_func = project.get_function('<function name>')
````
#### Run Function 
For run a function you will need to use the [run_function](https://docs.mlrun.org/en/latest/api/mlrun.projects.html?highlight=run_function#mlrun.projects.MlrunProject.run_function) method.
This method allows you to run a MLRun job locally and remotely as long as there is no requirments ( if there is any requirments you will need to build a new image)
It is equivalent to func.run method.
````
project.run_function(function='<function name>',params={'num':3},local=False)
````
````
project.run_function(function='<function name>',params={'num':3},local=True)
````
#### Build Function
For building a new image for MLRun jobs you will need to use the [build_function](https://docs.mlrun.org/en/latest/api/mlrun.projects.html?highlight=build_function#mlrun.projects.MlrunProject.build_function) method
This method allows you to build a new image based on your job requirements - this method it only for non remote function for example MLRun jobs.
It is equivalent to func.deploy method.
````
project.build_function('<function name>')
````

#### Deploy Function
For deplying remote function as nuclio and serving you will need to use the [deploy_function](https://docs.mlrun.org/en/latest/api/mlrun.projects.html?highlight=deploy_function#mlrun.projects.MlrunProject.deploy_function) method.
You must use this method beofre invoke nuclio and serving fucntions.
It is equivalent to func.deploy method.
````
nuclio_func=project.deploy_function(function='<function name>')

nuclio_func.function.invoke('/',{'int':4})
````

For more Examples you can see Load_project and load_project_clone
