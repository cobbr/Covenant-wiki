## Listeners

To get an operation started, you will want to start a new listener. Covenant supports native listeners and "bridge" listeners. This guide is for native listeners, the `BridgeListener` is discussed [here](https://github.com/cobbr/Covenant/wiki/Bridge-Listeners). Currently, the only built-in, native listener that Covenant supports is the `HttpListener`.

To create a new `Httplistener`, you'll first navigate to the Listeners navigation page:

![Listeners page](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-listeners.png)

Currently, there are no listeners in the listener table, but this will change once we create one. Click on the "Create" button to configure the listener:

![Create Listener](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-listenercreate.png)

The following options will need to be configured when creating the listener:

* **Name** - The `Name` of the listener that will be used throughout the interface. Pick something recognizable!
* **BindAddress** - The `BindAddress` is the local ip address that the listener will bind to. This can be helpful in cases where the Covenant host has multiple nics. Usually, this value will be `0.0.0.0`.
* **BindPort** - The `BindPort` is the local port that the listener will bind to.
* **ConnectPort** - The `ConnectPort` is the *callback* port that Grunts will be directly connecting to. This also represents the port portion of the `Urls`.
* **ConnectAddresses** - The `ConnectAddresses` are the *callback* addresses, and represents the hostname portion of the `Url`. You must specify at least one `ConnectAddress` and can specify as many as you would like. You can specify multiple `ConnectAddresses` for failure prevention. Grunts will attempt to connect to each of these `ConnectAddresses` and will use the first one that succeeds. If you are using redirectors, this should be the url that points to the external redirector.
* **Urls** - The `Urls` are the *callback* URLs, and are the urls that Grunts will be directly connecting to. The URLs are calculated based on a combination of the `ConnectAddresses`, `BindPort`, and `UseSSL` values, and should be of the form: `http(s)://<connectaddress>:<bindport>`. The `Urls` are calculated for you, you should not need to manually edit these values.
* **UseSSL** - The `UseSSL` value determines if the listener should use the HTTPS or HTTP protocol. If `UseSSL` value is true, an `SSLCertificate` needs to be provided.
* **SSLCertificate** - The `SSLCertificate` is the certificate used by the listener, if `UseSSL` is true. The certificate is expected be in PFX format.
* **SSLCertificatePassword** - The `SSLCertificatePassword` is the password that is being used to protect the `SSLCertificate`.
* **HttpProfile** - The `HttpProfile` determines the behavior of Grunt and Listener communication.

Once these options are configured, click on the "Create" button to start the listener. The newly active listener should now appear in the listeners table:

![Listener Table](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-listenercreated.png)

Listeners can be started and stopped by clicking on the listeners name within the listeners table. Selecting a listener will also reveal the detailed information about the listener that was configured earlier:

![Listener Info](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-listenerinfo.png)

You can start and stop the listener using the buttons at the bottom of the page.