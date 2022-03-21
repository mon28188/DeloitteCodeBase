# README DEMO #
## Introduction ##

Mijn PostNL is the online platform for PostNL Business Customers to pre-announce their parcels. Within the Business Portal customers can create and import shipments, validate the shipments and eventually print their barcode labels. It furthermore provides the customer with product information, a Track & Trace functionality and a module to maintain both their SMS and Email notifications.

## Wiki

The project wiki can be accessed [here](/wiki/Home.md).

### Projects ###

The following projects are included within this repository:

- Business Portal
- SKY Release 1

**Note**, SKY release 2 is currently being developed within a separate repository (PostNL-Commercial-SKY). Code for this project should not be stored within this repository. 

### Structure of the code base ###

Below is an overview of how the code base is structured:

```
root
   /documentation
   /lib
   /module_assets
   /patches
   /secondary_deploy
   /src
   build.properties
   build.xml
```

#### documentation ####

Inside the `documentation` folder you can find the automatically generated documentation of the code and several other components using MDoc. 

There are two sub-folders within the folder; `output` and `configuration`. The `output` folder contains the actual outputted documentation for which you can view offline. The `configuration` folder is used to stored the MDoc specific configuration for this project.

#### lib ####

This project implements continuous integration using Jenkins. When a job is ran on Jenkins to move code from one org to another it requires the use of the Force.com migration toolkit, which is versioned. The toolkit is stored within the repository to allow easy switching to a newer version without the need to modify the Jenkins jobs.
 

#### patches ####

When a hotfix is released to production patches are created by AMS and are provided back to the project teams to have them applied locally. The patches folder contains the patches which were originally supplied. Patches are stored in case they need to be reapplied in future in case of incidents or mistakes.

#### secondary_deploy ####

Certain aspects of the project cannot be deployed immediately due to manual steps being required before deploying. The project allows deploying the majority of the code base, followed by manual steps and then a secondary deploy is taken.

Although currently the secondary deploy is done manually it is still stored within the code base as a "separate" project to ensure we are tracking as much of the code base within the repository.

#### src ####

This is the main force.com project folder and will be deployed to each org.