# Deloitte Profile Utility Tool

---

#### Usage of this tool is mandatory when changing the profiles/permission sets.

For a project as big as PostNL with multiple Agile Streams and multiple production releases in a day, it becomes imperative that the Usage of Deloitte Profile Utility tool is mandatory. Any profile/permission set changes must be properly formatted using the tool before committing.

### Steps in Installation
1. Clone the Deloitte Profile Utility Repository locally from the location https://bitbucket.org/deloitte-nl-sfdc/faststart-profileutil  
   Reach out to steotia@Deloitte.nl/dvandelindt@Deloitte.nl for access issues.
2. Download NPM (if not present on your computer already). Refer to the URL - https://nodejs.org/en/download/  
   After successful installation, run the command `where npm` to verify that npm is installed.  
   Download Salesforce DX CLI from https://developer.salesforce.com/tools/sfdxcli
3. Open the Terminal in the location of the Profile Utility Repository and run the command `npm install`.  
   Next, run the command `sfdx plugins:link` to register the plugin with the DX CLI.  
   And you're ready to use Profile Utility Tool.

Here's where this tool can help: all you need to do is to specify the command, the path of your src folder, then the profiles/permission sets that you want
to update. Below is an example.

    sfdx profileutil:fields:add --path /Users/<userName>/<projectName>/src

### Profile Utility SFDX Commands

| Commands | Purpose |
| -------- | ------- |
| `profileutil:apex:add` | Adds apex classes to selected profiles and permission sets |
| `profileutil:apex:remove` | Removes apex classes from selected profiles and permission sets |
| `profileutil:applicationvisibilities:add` | Adds application visibilities to selected profiles and permission sets |
| `profileutil:applicationvisibilities:remove` | Removes application visibilities from selected profiles and permission sets |
| `profileutil:categoryGroupVisibilities:add` | Adds category group visibility to selected profiles and permission sets |
| `profileutil:categoryGroupVisibilities:remove` | Removes category group visibility from selected profiles and permission sets |
| `profileutil:customMetadataTypeAccesses:add` | Adds custom metadata type to selected profiles and permission sets |
| `profileutil:customMetadataTypeAccesses:remove` | Removes custom metadata type from selected profiles and permission sets |
| `profileutil:custompermissions:add` | Adds custom permissions to selected profiles and permission sets |
| `profileutil:custompermissions:remove` | Removes custom permissions from selected profiles and permission sets |
| `profileutil:fields:add` | Adds fields to selected profiles and permission sets |
| `profileutil:fields:remove` | Removes fields from selected profiles and permission sets |
| `profileutil:layoutassignments:add` | Adds layout assignments to selected profiles and permission sets |
| `profileutil:layoutassignments:remove` | Removes layout assignments from selected profiles and permission sets |
| `profileutil:loginipranges:add` | Adds login IP Ranges to selected profiles and permission sets |
| `profileutil:loginipranges:remove` | Removes login IP Ranges from selected profiles and permission sets |
| `profileutil:pages:add` | Adds pages to selected profiles and permission sets |
| `profileutil:pages:remove` | Removes pages from selected profiles and permission sets |
| `profileutil:recordtypevisibilities:add` | Adds record type visibilities to selected profiles and permission sets |
| `profileutil:recordtypevisibilities:remove` | Removes record type visibilities from selected profiles and permission sets |
| `profileutil:sobjects:add` | Adds sObjects to selected profiles and permission sets |
| `profileutil:sobjects:remove` | Removes sObjects from selected profiles and permission sets |
| `profileutil:tabvisibilities:add` | Adds tab visibilities to selected profiles |
| `profileutil:tabvisibilities:remove` | Removes tab visibilities from selected profiles |
| `profileutil:tabsettings:add` | Adds tab settings to permission sets |
| `profileutil:tabsettings:remove` | Removes tab settings from permission sets |
| `profileutil:userpermissions:add` | Adds user permissions to selected profiles and permission sets |
| `profileutil:userpermissions:remove` | Removes user permissions from selected profiles and permissions sets |
| `profileutil:util:format` | Formats one or more profiles or permission sets using the built in XLS stylesheets |
| `profileutil:util` | Collection of utility methods for managing profiles and permission sets |
| `Cat .\package.json` | Displays the json of all the available commands |


#### Sorting rules
- Special characters such as `" "`, `"."`, `"-"`, `"_"` are sorted first.
- Numbers are sorted before alphabetical characters.
- Capitals are sorted before lowercase.

---

[Home](/wiki/Home.md) - [Tools](/wiki/tools/tools.md) - Deloitte Profile Utility Tool