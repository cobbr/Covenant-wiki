## Data

The Data page displays certain types of information collected by Grunts during an operation, including credentials, indicators, and downloads.

Click on the "Data" navigation page to see the available data.

### Credentials

Credentials are automatically parsed from Grunt Task output if they can be identified. Passwords, password hashes, and Kerberos tickets are automatically parsed from Mimikatz and Rubeus output:

![Credentials](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-datacredentials.png)

Credentials can be manually added by clicking the "Create" button at the bottom of the page. Any of the credential types can be added:

![Create Credential](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-datacredentialcreate.png)

### Indicators

Indicators are automatically added as tasks are performed within Covenant. This information can be useful to provide to the Blue Team after an operation is complete, or for operators to keep track of the indicators they are leaving during operation.

To view the current indicators, click on the "Indicators" tab:

![Indicators](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-dataindicators.png)

There are three types of indicators tracked by Covenant:

* **Target Indicators** - `TargetIndicators` keep track of the systems that have been compromised. Whenever a new Grunt is established, the ComputerName and Username are added as a new TargetIndicator.
* **Network Indicators** - `NetworkIndicators` keep track of the listeners that have been used. Whenever a new Listener is activated, information about the Listener is added as a new NetworkIndicator.
* **File Indicators** - `FileIndicators` keep track of files that have been hosted or uploaded to a target system. Whenever a new file is hosted or a new file is uploaded to a target system, information about the file is added as a new FileIndicator.

Indicators can be manually added by clicking the "Create" button at the bottom of the page. Any of the indicator types can be added:

![Create Indicator](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-dataindicatorcreate.png)

### Downloads

Files can be downloaded from Grunts using the Download Task. Downloaded files will be available here for operators to download to their local file system:

![Downloads](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-datadownloads.png)