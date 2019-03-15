Covenant is a .NET command and control framework that aims to highlight the attack surface of .NET, make the use of offensive .NET tradecraft easier, and serve as a collaborative command and control platform for red teamers.

# Architecture

Covenant has a client-server architecture that allows for multi-user collaboration. There are three main components of Covenant’s architecture:

* Covenant - Covenant is the server-side component of the client-server architecture. Covenant runs the command and control server hosted on infrastructure shared between operators. I will also frequently use the term “Covenant” to refer to the entire overarching project that includes all components of the architecture.
* Elite - Elite is the client-side component of the client-server architecture. Elite is a command-line interface that operators use to interact with the Covenant server to conduct operations.
* Grunt - A “Grunt” is the name of Covenant’s implant that is deployed to targets.
All three components of Covenant are written in C#. Covenant and Elite both target .NET Core and have docker support, while Grunt implants target the .NET framework.

# Features
Covenant has a few key features that I think make it useful and differentiate it from some other command and control frameworks:

* Multi-Platform - Covenant and Elite both target .NET Core, which makes them multi-platform. This allows these programs to run natively on Linux, MacOS, and Windows platforms. Additionally, both Covenant and Elite have docker support, allowing these programs to run within a container on any system that has docker installed.
* Multi-User - Covenant supports multi-user collaboration. The ability to collaborate has become crucial for effective red team operations. Many users can start Elite clients that connect to the same Covenant server and operate independently or collaboratively.
* API Driven - Covenant is driven by a server-side API that enables multi-user collaboration and is easily extendible. Additionally, Covenant includes a Swagger UI that makes development and debugging easier and more convenient.
* Listener Profiles - Covenant supports listener “profiles” that control how the network communication between Grunt implants and Covenant listeners look on the wire.
* Encrypted Key Exchange - Covenant implements an encrypted key exchange between Grunt implants and Covenant listeners that is largely based on a similar exchange in the Empire project, in addition to optional SSL encryption. This achieves the cryptographic property of forward secrecy between Grunt implants.
* Dynamic Compilation - Covenant uses the Roslyn API for dynamic C# compilation. Every time a new Grunt is generated or a new task is assigned, the relevant code is recompiled and obfuscated with ConfuserEx, avoiding totally static payloads. Covenant reuses much of the compilation code from the SharpGen project, which I described in much more detail in a previous post.
* Inline C# Execution - Covenant borrows code and ideas from both the SharpGen and SharpShell projects to allow operators to execute C# one-liners on Grunt implants. This allows for similar functionality to that described in the SharpShell post, but allows the one-liners to be executed on remote implants.
* Tracking Indicators - Covenant tracks “indicators” throughout an operation, and summarizes them in the Indicators menu. This allows an operator to conduct actions that are tracked throughout an operation and easily summarize those actions to the blue team during or at the end of an assessment for deconfliction and educational purposes. This feature is still in it’s infancy and still has room for improvement.
* Developed in C# - Personally, I enjoy developing in C#, which may not be a surprise for anyone that has read my latest blogs or tools. Not everyone might agree that development in C# is ideal, but hopefully everyone agrees that it is nice to have all components of the framework written in the same language. I’ve found it very convenient to write the server, client, and implant all in the same language. This may not be a true “feature”, but hopefully it allows others to contribute to the project fairly easily.

# Usage

Covenant is designed to primarily be used with Docker, and the quick-start information is found in the Covenant readme and Elite readme. Following those instructions, you should launch Covenant on your shared C2 server, and launch the Elite client on your own machine, connecting it to the Covenant server.

While there is more detailed information available in the readmes, these are the basic commands to build Covenant and Elite docker containers to follow along with these usage instructions:

```
$ ~/Covenant/Covenant > docker build -t covenant .
$ ~/Covenant/Covenant > docker run -it -p 7443:7443 -p 80:80 -p 443:443 --name covenant covenant --username AdminUser --computername 0.0.0.0
$ ~/Elite/Elite > docker build -t elite .
$ ~/Elite/Elite > docker run -it --rm --name elite elite --username AdminUser --computername <covenant_ip>
```

When you first launch Elite, you’ll be prompted for a username, password, and certificate hash. After authenticating, you’ll be presented with the command-line interface. Using the help command, which can be used on any sub-menu in Elite, will let you know your options at the current menu or sub-menu:

![Elite Help](https://github.com/cobbr/Covenant/wiki/images/elite-menu-1.png)

# Listeners

You’ll see that you have a few options. The first thing you’ll want to do is to start a Listener. Navigating to the Listeners menu, you will see the types of listeners you have the option of using:

![Elite Listeners](https://github.com/cobbr/Covenant/wiki/images/elite-menu-2.png)

Currently, HTTP is the only supported type of listener, though I’ll be looking to add more in the future. The second, empty menu is the list of created listeners. We’ll see an entry added to this menu shortly.

Navigating to the HTTP menu, you are presented with options for the HTTP listener:

![Elite HTTP Listener](https://github.com/cobbr/Covenant/wiki/images/elite-menu-3.png)

When Covenant is operating within a Docker container, the BindAddress will often be 0.0.0.0, and the ConnectAddress may be the IP Address or domain name of the Covenant system or a redirector. You may also set the BindPort, a local SSL certificate, and an HttpProfile. You can then Start the listener and it will begin waiting for connecting Grunts:

![Elite HTTP Listeners](https://github.com/cobbr/Covenant/wiki/images/elite-menu-4.png)

You can also rename the Listener to something more convenient:

![Rename Listener](https://github.com/cobbr/Covenant/wiki/images/elite-menu-5.png)

# Launchers

Now that a Listener is started, you’ll want to navigate to the Launchers menu. The Launchers menu allows for the generation of one-liners or binaries/scripts that launch new Grunts. The Launchers menu is roughly organized by host binary name:

![Launchers Menu](https://github.com/cobbr/Covenant/wiki/images/elite-menu-6.png)

As an example, we’ll choose the PowerShell launcher. We are presented with options for the launcher, and set the Listener to the one we set up previously:

![PowerShell Launcher](https://github.com/cobbr/Covenant/wiki/images/elite-menu-7.png)

We have several options for generating the launcher. The simplest option, generate, generates a pre-staged powershell one-liner that ends up being fairly long and complex:

![PowerShell Generate](https://github.com/cobbr/Covenant/wiki/images/elite-menu-8.png)

We can also choose to host the PowerShell stager and generate a shorter, non-staged PowerShell one-liner that does a simple “download cradle”:

![PowerShell Host](https://github.com/cobbr/Covenant/wiki/images/elite-menu-9.png)

Finally, there’s the more generic code command that returns the C# stager and/or grunt code that could be used for more customized launch scenarios:

![Code](https://github.com/cobbr/Covenant/wiki/images/elite-menu-10.png)

And as always, the help command will give you more information about all the options available:

![PowerShell Help](https://github.com/cobbr/Covenant/wiki/images/elite-menu-11.png)

# Grunts

Executing a launcher on a system that successfully connects back to the Covenant listener results in a Grunt, Covenant’s implant, being activated:

![Grunt Activated](https://github.com/cobbr/Covenant/wiki/images/elite-menu-12.png)

Navigating to the Grunts menu shows a list of all activated Grunts and some key information about each. Using the interact command, we can interact with individual Grunts and conduct further actions. Navigating to this menu will display a few other settings applied to the Grunt:

![Grunt Menu](https://github.com/cobbr/Covenant/wiki/images/elite-menu-13.png)

The help command in this menu will display the built-in post-exploitation options for a Grunt:

![Grunt Interact Menu](https://github.com/cobbr/Covenant/wiki/images/elite-menu-14.png)

If you’ve ever used the SharpSploit project, hopefully you recognize some of these options. SharpSploit is tightly integrated with Covenant, allowing for the easy use of its most practical functions within a Grunt. This includes executing shell commands, PowerShell commands, mimikatz commands, etc:

![Grunt Interact Menu](https://github.com/cobbr/Covenant/wiki/images/elite-menu-15.png)

Grunts have another interesting built-in command, sharpshell, that combines some features of the SharpGen and SharpShell projects to allow for the execution of inline C# code that compiles against the SharpSploit library:

![SharpShell](https://github.com/cobbr/Covenant/wiki/images/elite-menu-16.png)
