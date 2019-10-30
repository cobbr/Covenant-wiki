## Bridge Listeners

To get an operation started, you will want to start a new listener. Covenant supports native listeners and "bridge" listeners. This guide is for bridge listeners, native listeners are discussed [here](https://github.com/cobbr/Covenant/wiki/Listeners).

A `BridgeListener` is used to communicate with a [C2Bridge](https://github.com/cobbr/C2Bridge). A C2Bridge provides an outbound C2 protocol that Grunts will communicate with. A `BridgeListener` is a simple TCP connection that allows a C2Bridge to communicate the C2 traffic with Covenant. This guide is for the `BridgeListener`, C2Bridges are discussed [here](https://github.com/cobbr/Covenant/wiki/C2Bridges).

To create a new `BridgeListener`, you'll first navigate to the Listeners navigation page:

![Listeners page](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-listeners.png)

Currently, there are no listeners in the listener table, but this will change once we create one. Click on the "Create" button to configure the listener, and select the "BridgeListener" tab:

![Create Bridge Listener](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-bridgelistenercreate.png)

The following options will need to be configured when creating the listener:

* **Name** - The `Name` of the listener that will be used throughout the interface. Pick something recognizable!
* **BindAddress** - The `BindAddress` is the local ip address that the listener will bind to. This can be helpful in cases where the Covenant host has multiple NICs. Usually, this value will be `0.0.0.0`.
* **BindPort** - The `BindPort` is the local port that the listener will bind to. This is the port that the C2Bridge will connect to.
* **ConnectPort** - The `ConnectPort` is the *callback* port that Grunts will be directly connecting to. This is the port the C2Bridge should listen on.
* **ConnectAddress** - The `ConnectAddress` is the *callback* address that Grunts will be directly connecting to. This should be the external address of the C2Bridge, or if you are using redirectors this should be the address that points to the external redirector.
* **BridgeProfile** - The `BridgeProfile` determines the behavior of Grunt and Listener communication. **The profile must specify BridgeMessengerCode that is compatible with the C2Bridge you choose to use.**

Once these options are configured, click on the "Create" button to start the listener. The newly active listener should now appear in the listeners table:

![Listener Table](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-bridgelistenercreated.png)

Listeners can be started and stopped by clicking on the listener's name within the listeners table. Selecting a listener will also reveal the detailed information about the listener that was configured earlier:

![Listener Info](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-bridgelistenerinfo.png)

You can start and stop the listener using the buttons at the bottom of the page.