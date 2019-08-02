## Listeners

To get an operation started, you will want to start a new listener. Currently, Covenant supports HTTP listeners only.

To create a new HTTP listener, you'll first navigate to the Listeners navigation page:

![Listeners page](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-listeners.png)

Currently, there are no listeners in the listener table, but this will change once we create one. Click on the "Create" button to configure the listener:

![Create Listener](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-listenercreate.png)

The following options will need to be configured when creating the listener:

* **Name** - The `Name` of the listener that will be used throughout the interface. Pick something recognizable!
* **Url** - The `Url` is the *callback* URL, and is the url that Grunts will be directly connecting to. If you are using redirectors, this should be the url that points to the external redirector. The URL should be a combination of the `ConnectAddress`, `BindPort`, and `UseSSL` values, and should be of the form: `http(s)://<connectaddress>:<bindport>`.
* **ConnectAddress** - The `ConnectAddress` is the *callback* address, and represents the hostname portion of the `Url`.
* **BindAddress** - The `BindAddress` is the local ip address that the listener will bind to. This can be helpful in cases where the Covenant host has multiple nics. Usually, this value will be `0.0.0.0`.
* **BindPort** - The `BindPort` is the local port that the listener will bind to. This also represents the port portion of the `Url`.
* **UseSSL** - The `UseSSL` value determines if the listener should use the HTTPS or HTTP protocol. If `UseSSL` value is true, an `SSLCertificate` needs to be provided.
* **HttpProfile** - The `HttpProfile` determines the behavior of Grunt and listener communication.
* **SSLCertificate** - The `SSLCertificate` is the certificate used by the listener, if `UseSSL` is true. The certificate is expected be in PFX format.
* **SSLCertificatePassword** - The `SSLCertificatePassword` is the password that is being used to protect the `SSLCertificate`.

Once these options are configured, click on the "Create" button to start the listener. The newly active listener should now appear in the listeners table:

![Listener Table](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-listenercreated.png)

Listeners can be started and stopped by clicking on the listeners name within the listeners table. Selecting a listener will also reveal the detailed information about the listener that was configured earlier:

![Listener Info](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-listenerinfo.png)

You can start and stop the listener using the buttons at the bottom of the page.