Covenant is a .NET command and control framework and web application that aims to highlight the attack surface of .NET, make the use of offensive .NET tradecraft easier, and serve as a collaborative command and control platform for red teamers.

# Wiki

1. [Installation and Startup](https://github.com/cobbr/Covenant/wiki/Installation-And-Startup)
2. [User Management](https://github.com/cobbr/Covenant/wiki/User-Management)
3. [Listener Profiles](https://github.com/cobbr/Covenant/wiki/Listener-Profiles)
4. [Listeners](https://github.com/cobbr/Covenant/wiki/Listeners)
5. [Launchers](https://github.com/cobbr/Covenant/wiki/Launchers)
6. [Grunt Interaction](https://github.com/cobbr/Covenant/wiki/Grunt-Interaction)
7. [Building Tasks](https://github.com/cobbr/Covenant/wiki/Building-Tasks)
8. [Graph View](https://github.com/cobbr/Covenant/wiki/Graph-View)
9. [Data](https://github.com/cobbr/Covenant/wiki/Data)
10. [Task Contribution Guide](https://github.com/cobbr/Covenant/wiki/Task-Contribution-Guide)
11. [C2Bridges](https://github.com/cobbr/Covenant/wiki/C2Bridges)
12. [Bridge Listeners](https://github.com/cobbr/Covenant/wiki/Bridge-Listeners)
13. [Using the API](https://github.com/cobbr/Covenant/wiki/Using-The-API)

# Features

Covenant has several key features that make it useful and differentiate it from other command and control frameworks:

* **Intuitive Interface** - Covenant provides an intuitive web application to easily run a collaborative red team operation.
* **Multi-Platform** - Covenant targets .NET Core, which is multi-platform. This allows Covenant to run natively on Linux, MacOS, and Windows platforms. Additionally, Covenant has docker support, allowing it to run within a container on any system that has docker installed.
* **Multi-User** - Covenant supports multi-user collaboration. The ability to collaborate has become crucial for effective red team operations. Many users can interact with the same Covenant server and operate independently or collaboratively.
* **API Driven** - Covenant is driven by an API that enables multi-user collaboration and is easily extendible. Additionally, Covenant includes a Swagger UI that makes development and debugging easier and more convenient.
* **Listener Profiles** - Covenant supports listener “profiles” that control how the network communication between Grunt implants and Covenant listeners look on the wire.
* **Encrypted Key Exchange** - Covenant implements an encrypted key exchange between Grunt implants and Covenant listeners that is largely based on a similar exchange in the Empire project, in addition to optional SSL encryption. This achieves the cryptographic property of forward secrecy between Grunt implants.
* **Dynamic Compilation** - Covenant uses the Roslyn API for dynamic C# compilation. Every time a new Grunt is generated or a new task is assigned, the relevant code is recompiled and obfuscated with ConfuserEx, avoiding totally static payloads. Covenant reuses much of the compilation code from the SharpGen project, which I described in much more detail in a previous post.
* **Inline C# Execution** - Covenant borrows code and ideas from both the SharpGen and SharpShell projects to allow operators to execute C# one-liners on Grunt implants. This allows for similar functionality to that described in the SharpShell post, but allows the one-liners to be executed on remote implants.
* **Tracking Indicators** - Covenant tracks “indicators” throughout an operation, and summarizes them in the Indicators menu. This allows an operator to conduct actions that are tracked throughout an operation and easily summarize those actions to the blue team during or at the end of an assessment for deconfliction and educational purposes. This feature is still in it’s infancy and still has room for improvement.
* **Developed in C#** - Personally, I enjoy developing in C#, which may not be a surprise for anyone that has read my latest blogs or tools. Not everyone might agree that development in C# is ideal, but hopefully everyone agrees that it is nice to have all components of the framework written in the same language. I’ve found it very convenient to write the server, client, and implant all in the same language. This may not be a true “feature”, but hopefully it allows others to contribute to the project fairly easily.
