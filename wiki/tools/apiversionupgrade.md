# API Version Upgrade Tool

---

#### Easy to use tool for upgrading API versions of Salesforce meta xml files!

Periodically, Salesforce comes up with a new release(api version) which brings new features, improvements and bug fixes.
For a project having hundreds of components, only upgrading that version on the meta xml files takes way longer than it should.

Here's where this tool can help: all you need to do is to specify the path of your src folder, then specify which components you want
to upgrade and then the source and target api version.

    Since this is an SFDX plugin, it is a pre-requisite to have Salesforce CLI installed globally first.

Using the plugin:
1. Install the plugin: `sfdx plugins:install salesforce-apiversion-upgrade`
2. See available commands by running: `sfdx metadatautil:upgradeapiversion`

```
USAGE:
$ sfdx metadatautil:upgradeapiversion -m <array> -p <string> [-s <number>] [-t <number>] [-x <string>] [-d] [--json]
[--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

OPTIONS:
-d, --dryrun If present will only output the files changed without actually changing them
-m, --metadata (required) Select metadata type. Possible values:  classes/pages/components/triggers/aura/lwc
-p, --path (required) The path to your src folder
-s, --sourceversion The API version threshold from which you wish to upgrade. Minimum: 10, Maximum: 50, Default: 50
-t, --targetversion The API version you want to upgrade to. Minimum:30 Maximum:51 Default:51
-x, --fileprefix Metadata filename prefix. E.g. App for App_Utils.cls. Default: none(all files)

EXAMPLES:
sfdx metadatautil:upgradeapiversion -m classes -s 40 -t 48 -p "C:\Users\SSSS\Project\src"
sfdx metadatautil:upgradeapiversion -m classes/pages -s 40 -t 48 -p "C:\Users\SSSS\Project\src" -x "App"
```

Repository is public and can be accessed [here](https://github.com/ganesh2109/salesforce-apiversion-upgrade)

---

[Home](/wiki/Home.md) - [Tools](/wiki/tools/tools.md) - API Version Upgrade Tool