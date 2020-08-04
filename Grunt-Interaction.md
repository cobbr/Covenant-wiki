## Grunt Interaction

Grunts are Covenant's C# implant. Most of an operator's time will be spent interacting with grunts to assign tasks and collect information.

Click on the Grunt navigation page to see a list of active grunts:

![Grunts Table](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-grunts.png)

You can interact with Grunts through either the tabbed terminal view or in the detailed, full-screen interaction view.

For the tabbed terminal view, click the small terminal icon next to the entry in the Grunt table to activate a Grunt into the tabbed terminal view below. This view makes it easy to operate when quickly switching between multiple implants.

![Tabbed Terminal](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-grunts-tabbed.png)

For the detailed interaction view, click on the name of the Grunt you would like to interact with, and this will bring you to a detailed page with all of the grunt's information:

![Grunt Info](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-gruntinfo.png)

The Grunt page includes four main tabs, each used for a different purpose:

* **Info** - The Info tab displays all the detailed information about the Grunt. This includes information about the implant as well as information about the user and system on which the implant is running. You are also able to edit some of the Grunt's information on this page. You can edit the Name, Note, Delay, JitterPercent, ConnectAttempts, and KillDate from this page. Keep in mind that editting the Delay, JitterPercent, or KillDate results in a task being assigned to the Grunt.
* **Interact** - The Interact tab provides a command-line like interface. Operators will likely spend most of their time in this interface. The interface is scrollable and vertically resizable, command suggestions are tab-completable as you type, and you will see updates in real-time so that you can see what other operators are doing.
* **Task** - The Task tab provides a dropdown dialog where an operator can select a specific task to be executed and fill in parameters in dialog boxes. The Task tab provides an alternative interface for assigning Tasks purely through a GUI. This view enables operators that are not comfortable with the command-line interface, or if command-line parsing is giving an operator some trouble.
* **Taskings** - The Taskings tab shows the grunt's command histroy in a searchable, table view. This allows an operator to click on taskings to get more detailed information for any specfici tasking, task, or user.