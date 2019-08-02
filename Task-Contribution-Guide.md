Covenant has many built-in tasks that allows for extending the capability of the Grunt implant. Tasks can be simple convenience functions or more complex or advanced features. Tasks are a great way for outstide contributors to add new tools, tradecraft, or capabilities to Covenant.

Contributing Tasks to Covenant is fairly simple, thought not quite as simple as I would like. This is a brief `Task Contribution Guide` meant to make contributing as straightforward and step-by-step as possible.

##  Step 1 - How large is your task?

Does your new task require a lot of code and/or is fairly complex?

If so, this may change the way you contribute to Covenant. If your task does not fit well into a single source file, then consider adding your task as a `git` submodule to Covenant. Submodules are found under the `Covenant/Covenant/Data/Tasks/src` folder.

If your task does not fit in a single source file and you do not have another git project to add as a submodule or don't want to deal with the headache of adding git submodules, please consider contributing to [SharpSploit](https://github.com/cobbr/SharpSploit)! `SharpSploit` is a library of C# post-exploitation functions. If your task fits well within the SharpSploit project, this is a great way to contribute your task/library to Covenant. For example, we'll take a Pull Request from Dennis Panagiotopoulos ([@den_n1s](https://twitter.com/den_n1s)) that added a COM hijacking persitence module:

![SharpSploit COM Hijack](https://github.com/cobbr/Covenant/wiki/images/sharpsploit-pull-request.png)

## Step 2 - The .task file

Once you have added your task's source library as a submodule or added it to `SharpSploit` (or if this is not necessary for your task), the next step is to create a `.task` file. You will find many examples of `.task` files under the `Covenant/Covenant/Data/Tasks` folder. The code defined in the `.task` file is what will be executed on the Grunt implant when you assign the task.

You will need to create a new `.task` file that is a C# source file that implements a class named `Task` with a method named `Execute()` that returns a `string`. You may define as many parameters as needed to this method, but each of these parameters should be of type `string`. You will need to do whatever conversions necessary on these parameters to create objects of the correct types that are needed for the task. These parameters are what will need to be defined by an operator prior to executing the `Task`, which is why the parameters must be defined as strings.

You may import libraries from any `SharpSploit` namespaces or namespaces from your added `git` submodules. You can also define any auxilliary classes or methods within this file that is needed to perform your task. However, the `Task.Execute()` method is what will get called by the Grunt implant when the task is executed.

Again, we'll take the COM hijacking persistence task as an example:

![Persist COM Hijack Task](https://github.com/cobbr/Covenant/wiki/images/persist-com-hijack-task.png)

## Step 3 - Adding your task to the database

You will need to edit the `Covenant/Covenant/Data/DbInitializer.cs` file to add the task to the Covenant database. There is a `List<GruntTask>` named `GruntTasks` in this file, in the `InitializeTasks()` method. You will need to add a new `GruntTask` object to this list. There are many examples in this file to use as references.

You will need to be sure to add a list of `GruntTaskOption`s that correspond to the parameters that are expected to be passed to your `Task.Execute()` function. There is also a `value` field that can be defined to provide a default option, feel free to define these where it might make sense.

Again, we'll take the COM hijacking persistance task as an example:

![Task DbInit Example](https://github.com/cobbr/Covenant/wiki/images/task-dbinit-example.png)

## Step 4 - Use your task!

Those are the only steps necessary to use your task. Now you can start up Covenant, and assign your task to active Grunts.

# Wanted Tasks

Looking for inspiration for new tasks? Here are a few ideas for tasks that would be valuable additions:

* Process Migration
* Screenshot
* Keylogging
* Persistence Tasks