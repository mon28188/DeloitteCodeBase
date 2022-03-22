# Destructive changes

---
To delete components, remove the component from the project repository and add it in the `destructive changes` manifest file.

In Summer '15 Salesforce introduced this way for developers to manage their destructive changes; `destructiveChangesPre.xml` and `destructiveChangesPost.xml`. When a deployment is done Salesforce will automatically process both of these files (if they exist) and will destroy all of the components listed within them.

Two files can be used for managing destructive changes; one for before the deployment takes place (pre) and one for after (post). The most common way of managing destructive changes is through using the `destructiveChangesPost.xml` file. Both files are the same in their structure and are only executed at different moments.

> ***TIP:*** the `destructiveChangesPre.xml` and `destructiveChangesPost.xml` should reside in the same folder as the `package.xml` file.

## How do the destructive changes files work?

If you have seen the `package.xml` before within your project you will be very familiar with the destructive changes files.

```
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
	
    <types>
        <members>BPG_Address</members>
        <name>ApexClass</name>
    </types>
    
    <types>
        <members>DEX_Installation_Management_VFC</members>
        <members>SEL_DEX</members>
        <name>ApexClass</name>
    </types>
    
    <types>
        <members>DEX__c</members>
        <members>Dex_Settings__c</members>
        <name>CustomObject</name>
    </types>

    <types>
        <members>Dex_Settings__c-nl_NL</members>
        <members>DEX__c-en_US</members>
        <members>DEX__c-nl_NL</members>
        <name>CustomObjectTranslation</name>
    </types>
    
</Package>
```

Components will be destroyed based on their name and their component type. So, if we wanted to delete an Apex class named as `BPG_Address` then we would add it as a `members` entry within a `types` section which contains the component name `ApexClass`.

> Notice that you can have repeated types with the same name defined within the destructive changes.

---

[Home](/wiki/Home.md) - [Deployment](/wiki/deployment/deployment.md) - Destructive changes