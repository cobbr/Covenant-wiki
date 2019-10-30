## Listener Profiles

Covenant supports listener profiles that control the network communication between listeners and grunts.

Before starting an operation, you may want to edit or develop new profiles to customize network traffic to blend in on a target network. To edit or create a new listener profile, navigate to the listeners navigation page and select the "Profiles" tab:

![Profiles Table](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-profiles.png)

To create a new profile, click on the "Create" button. To edit a particular profile, click on the name of the profile. Keep in mind, that you cannot edit profiles that are associated with active listeners.

After clicking "Create" or selecting a profile to edit, you will be able to configure the profile:

![Profile Configure](https://github.com/cobbr/Covenant/wiki/images/covenant-gui-profileedit.png)

The following options will need to be configured when editing or creating a profile:

* **Name** - The `Name` of the profile that will be used throughout the interface. Pick something recognizable!
* **Description** - The `Description` of the profile. This should be a thorough description of the profile that operators can read and easily understand how the profile works, and the use cases for which it would be appropriate to use the profile. 
* **MessageTransform** - The `MessageTransform` is a unique way to specify how the communication data will be transformed before being placed into the formats specified in the `HttpPostRequest`, `HttpGetResponse`, and `HttpPostReponse`. An `MessageTransform` should be a static C# class named `MessageTransform` that includes a public `Transform` and a public `Invert` function. The class can transform the data in any way that you desire, as long as the Transform and Invert functions mirror each other (i.e. `data == MessageTransform.Invert(MessageTransform.Transform(data))`). The `MessageTransform` class must be cross-platform compatible and compile under `Net40`, `Net35`, and `NetCore21`.
* **HttpUrls** - The `HttpUrls` is a list of one or more urls that grunts will callback to, including any query parameters. A grunt will randomly select one of these urls each time it polls the server. The grunt GUID must be present in either a query string in *each* HttpUrl **or** in a single HttpRequestHeader, in either the name or value field. To specify the GUID in the HttpUrls, include the string "{GUID}" in a **query string** to indicate the location that the GUID should be placed.
* **HttpRequestHeaders** - The `HttpRequestHeaders` are name/value pairs that will be included as HTTP request headers in HTTP requests from grunts to the listener. Every header will be included in every request. The grunt GUID must be present in either the name or value field of one of the headers **or** in the query string of *each* HttpUrl. The specify the GUID in an HttpRequestHeader, include the string "GUID" in a header name or value to indicate the location that the GUID should be placed.
* **HttpResponseHeaders** - The `HttpResponseHeaders` are name/value pairs that will be includes as HTTP response headers in HTTP responses from the listener to grunts. Every header will be included in every response.
* **HttpPostRequest** - The `HttpPostRequest` is the format of the HTTP request when a grunt posts data back to a listener. The format must include a location for the data to be placed. Include the string "{0}" to indicate the location that the data should be placed.
* **HttpGetResponse** - The `HttpGetResponse` is the format of the HTTP response when a grunt polls a listener for tasks. The format must include a location for the data to be placed. Include the string "{0}" to indicate the location that the data should be placed.
* **HttpPostResponse** - The `HttpPostResponse` is the format of the HTTP response when a grunt posts data to a listener. The format must include a location for the data to be placed. Include the string "{0}" to indicate the location that the data should be placed.

Click the "Edit" or "Create" button to finalize any changes made to a profile.