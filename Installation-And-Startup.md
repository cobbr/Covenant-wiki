## Installation

Be sure to clone Covenant recursively to initialize the git submodules: `git clone --recurse-submodules https://github.com/cobbr/Covenant`

### Option 1 - Dotnet Core

The easiest way to use Covenant is by installing dotnet core. You can download dotnet core for your platform from [here](https://dotnet.microsoft.com/download/dotnet-core/3.1).

Be sure to install the dotnet core version **3.1 SDK**!

Once you have installed dotnet core, we can build and run Covenant using the dotnet CLI:

```
$ ~ > git clone --recurse-submodules https://github.com/cobbr/Covenant
$ ~ > cd Covenant/Covenant
$ ~/Covenant/Covenant > dotnet run
warn: Microsoft.EntityFrameworkCore.Model.Validation[10400]
      Sensitive data logging is enabled. Log entries and exception messages may include sensitive application data, this mode should only be enabled during development.
WARNING: Running Covenant non-elevated. You may not have permission to start Listeners on low-numbered ports. Consider running Covenant elevated.
Covenant has started! Navigate to https://127.0.0.1:7443 in a browser
```

### Option 2 - Docker

Covenant can also be run with Docker. There are a couple of gotchas with Docker, so we only recommend using docker if you are familiar with docker or are willing to learn the subtle gotchas.

First, build the docker image:

```
$ ~ > git clone --recurse-submodules https://github.com/cobbr/Covenant
$ ~ > cd Covenant/Covenant
$ ~/Covenant/Covenant > docker build -t covenant .
```

Now, run Covenant within the Docker container (be sure to replace the "</absolute/path/to/Covenant/Covenant/Data>" with your own absolute path!):

```
$ ~/Covenant/Covenant > docker run -it -p 7443:7443 -p 80:80 -p 443:443 --name covenant -v </absolute/path/to/Covenant/Covenant/Data>:/app/Data covenant
```

The `-it` parameter is a Docker parameter that indicates that we should begin Covenant in an interactive tty, and can be excluded if you would not like to attach to the tty.

The `-p` parameters expose ports to the Covenant Docker container. You must expose port 7443 and any other ports you would like to start listeners on.

The `-v` parameter creates a shared Data directory between the host and the container. Be sure to specify an absolute path to your data directory, a relative path will not work.

Once Covenant has been started, you can disconnect from the interactive interface at any time by pressing `Ctrl+p` and `Ctrl+q` consecutively.

To stop the container, you can run:

```
$ ~/Covenant/Covenant > docker stop covenant
```

And to restart Covenant interactively (with all data saved), you can run:

```
$ ~/Covenant/Covenant > docker start covenant -ai
```

Alternatively, to remove all Covenant data and restart fresh, you can remove and run again (again, be sure to replace the "</absolute/path/to/Covenant/Covenant/Data>" with your own absolute path!):

```
$ ~/Covenant/Covenant > docker rm covenant
$ ~/Covenant/Covenant > docker run -it -p 7443:7443 -p 80:80 -p 443:443 --name covenant -v </absolute/path/to/Covenant/Covenant/Data>:/app/Data covenant --username AdminUser --computername 0.0.0.0
```

## Registration

After starting Covenant, you must register an initial user through the web interface. Navigating to the web interface will allow you to register the initial user:

![User Registration](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-registration.png)

Once the initial user has been registered, open registration will be closed, and new users will have to be created by an Administrative user.
