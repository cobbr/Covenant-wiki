Defense against C# and, more generally, .NET tradecraft has been a frequently discussed topic over the last year or so. The good news is that the options for defenders seems to be increasing.

While there doesn’t appear to be any official Microsoft documentation on the subject, an undocumented ETW provider may be used to capture loaded assemblies and AppDomains, which was discovered by Matt Graeber (@mattifestation) and I discussed in my last post. Matt has also published a PoC PowerShell script for capturing relevant .NET runtime artifacts that is available here.

Additionally, the AMSI (Antimalware Scan Interface) has officially been added to .NET 4.8, which may increase the insights of security products into .NET assemblies loaded from locations other than disk. I’ve posted extensively on the topic of AMSI as it relates to PowerShell, and I imagine it will have similar effects on .NET tradecraft in the future. .NET 4.8 is still in the “early access” phase of development, so it may be some time before organizations have deployed .NET 4.8 throughout the enterprise. However, the sooner an organization can do so, the better.

These methods of detection and prevention will certainly be effective against Covenant specifically. Covenant is almost entirely reliant on the System.Reflection.Assembly.Load() function. AMSI in .NET will certainly target assemblies loaded in this manner.

Additionally, Covenant attempts to track some of the more traditional indicators that are not specific to .NET. As you operate within Covenant, it tracks domain names you use, files you generate, etc.

Navigating to the Indicators menu you will see the indicators that Covenant has tracked:

[Indicators]

Covenant tracks TargetIndicators, the computers and users you have established Grunt implants on, NetworkIndicators, listeners you have started, and FileIndicators, files that you have hosted on your listener.

The idea behind tracking indicators is to allow operators to conduct actions and easily summarize those actions to the blue team during or at the end of an assessment. Covenant’s capability for tracking indicators has a lot of room for improvement, and this is a feature I will continue to enhance. Eventually, I would love to track many other types of indicators and incorporate some sort of report generation.

