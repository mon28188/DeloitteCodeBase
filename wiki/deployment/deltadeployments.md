# Delta deployments

---
Working on a Salesforce project, the key to improve the speed, reliability and quality of the deployments is having a source-based release management process described by Continuous Integration.

### Incremental deployments 

One of the most important point in the way our project works is the incremental deployments. All our pipelines present tags (e.g. UATREFRESH, PRODUCTION, DFMTEST, MPNLTEST etc) characterized by a number that increments everytime a deployment was successfully performed via a pipeline job. In this way, the delta deployment knows to pick up in the package only the components that have been modified since the last time the tag was incremented, more specifically, since the last deployment in the respective environment was performed.

### Settings for the delta deployments

For the automatic creation of the package.xml file, the metadata types have to be properly defined in the properties files that can be found at the following destinations:

* **build/deploy/config.properties** 
* **build_cicd/modules/deltadeployments/config.properties**

In the files, one can found instructions for a correct definition.

_**Note**:_ After PostNL project will be migrated to DROP, this settings will not be needed anymore as the metadata types will be defined at the library level.

---

[Home](/wiki/Home.md) - [Deployment](/wiki/deployment/deployment.md) - Delta deployments