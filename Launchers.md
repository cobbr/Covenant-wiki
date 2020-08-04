## Launchers

Launchers are used to generate, host, and download binaries, scripts, and one-liners to launch new Grunts.

Once a listener has been started, you'll want to generate a launcher to use in kicking off Grunts. To get started, navigate to the Launchers navigation page:

![Launchers Table](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-launchers.png)

Launchers are named roughly by the system binary that will be used to execute the launcher. Currently, Covenant supports the following launchers:

* **Binary** - The `Binary` launcher is used to generate custom binaries that launch a Grunt. This is currently the only launcher that does not rely on a system binary.
* **ShellCode** - The `ShellCode` launcher converts a Grunt binary to ShellCode using Donut.
* **PowerShell** - The `PowerShell` launcher is used to generate PowerShell code and/or a PowerShell one-liner that launches a Grunt using `powershell.exe`.
* **MSBuild** - The `MSBuild` launcher is used to generate an MSBuild XML file that launches a Grunt using `msbuild.exe`.
* **InstallUtil** - The `InstallUtil` launcher is used to generate an InstallUtil XML file that launches a Grunt using `installutil.exe`.
* **Mshta** - The `Mshta` launcher is used to generate an HTA file and/or a mshta one-liner that launches a Grunt using `mshta.exe` that relies on DotNetToJScript.
* **Regsvr32** - The `Regsvr32` launcher is used to generate an SCT file and/or regsvr32 one-liner that launches a Grunt using `regsvr32.exe` that relies on DotNetToJScript.
* **Wmic** - The `Wmic` launcher is used to generate an xsl file and/or wmic one-liner that launches a Grunt using `wmic.exe` that relies on DotNetToJScript.
* **Cscript** - The `Cscript` launcher is used to generate a JScript file a Grunt using `cscript.exe` that relies on DotNetToJScript.
* **Wscript** - The `Wscript` launcher is used to generate a JScript file a Grunt using `wscript.exe` that relies on DotNetToJScript.

Please keep in mind that any of the launchers that rely on DotNetToJScript **may not work** on some of the latest versions of Windows 10 and Windows Server 2016 and/or may be signatured by some AMSI providers.

## Binary Launcher

To generate a binary launcher, click on the "Binary" link within the launchers table. This will reveal some configuration options to consider before you generate the launcher:

![Binary Launcher Options](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-launcherbinary.png)

Other launchers may have some additional configuration options, but these options are common to all launcher types. The configuration options to consider are:

* **Listener** - The `Listener` is the name of the listener that this Grunt should communicate with. If you have multiple active listeners, be sure to select the correct listener.
* **ImplantTemplate** - The `ImplantTemplate` is the type of implant that the launcher will generate.
* **DotNetVersion** - The `DotNetVersion` of the implant that will be generated. You'll be limited to a choice of the `DotNetVersion`s compatible with the chosen `ImplantTemplate`.
* **Delay** - The `Delay` is the time that the Grunt will sleep in-between each poll of the server. A larger `Delay` value will result in stealthier communication, but increase the time it takes to task a Grunt.
* **JitterPercent** - The `JitterPercent` is the percentage of variability in the `Delay` value.
* **ConnectAttempts** - The `ConnectAttempts` is the number of consective times a Grunt will attempt to poll the listener before quitting. If a Grunt cannot reach the listener and fails to successfully poll the listener more times than the `ConnectAttempts` value, it will quit.
* **KillDate** - The `KillDate` is the date at which a Grunt will quit and stop calling back to the listener.


Some other options may be displayed based upon the `ImplantTemplate` that has been selected. If you select an `ImplantTemplate` with an `HTTP` `CommType`:

* **ValidateCert** - The `ValidateCert` option determines if the Grunt will validate the listener's SSL certificate to prevent MiTM attacks. There are scenarios where target network proxies can interfere with certificate validation, and it's preferrable to *not* validate the certificate. This option is only relavent when using the HTTP `CommType`, and will only be displayed if you have selected the HTTP `CommType`.
* **UseCertPinning** - The `UseCertPinning` option determines if the Grunt will use cert pinning of the listener's SSL certificate to prevent MiTM attacks. There are scenarios where target network proxies can interfere with certificate pinning, and it's preferrable to *not* perform cert pinning. This option is only relavent when using the HTTP `CommType`, and will only be displayed if you have selected the HTTP `CommType`.

If you select an `ImplantTemplate` with an `SMB` `CommType`:

* **SMBPipeName** - The `SMBPipeName` is the name of the named pipe that the Grunt will bind to and listen on. This option is only relavent when using the SMB `CommType`, and will only be displayed if you have selected the SMB `CommType`.

Once the options are configured as desired, click the "Generate" button to generate the launcher. Now that the launcher is generated, you can choose to download the launcher to a local file or host the launcher on the listener. **You must generate the launcher prior to downloading or hosting**.

To download the launcher to a local file, click the "Download" button.

### Host Launcher

To host the launcher, click on the "Host" tab. This will provide a Url option:

![Host Launcher](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-launcherhost.png)

Choose a URL at which you would like to host the launcher and click the "Host" button to host.

### Launcher Code

You may wish to view the source code of the launcher's `GruntStager`. To view the code click on the "Code" tab:

![Launcher Code](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-launchercode.png)

You can use this code to create a custom Grunt that does not utilize any of the built-in launchers. Click the "Copy" button to copy the code to the clipboard.