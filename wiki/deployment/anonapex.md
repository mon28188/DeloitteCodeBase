# Anonymous apex scripts

---

It is advised to avoid as much as possible the manual steps at deployments.
Depending on the requirement, we can automate the step in all environments by creating these Anonymous Apex scripts.  
The general purpose is to perform changes on data, not on metadata.

## File location

The Anonymous Apex scripts are stored in the folder `data/apexscript` and these run on all deployments.
Changes in this folder are automatically detected and executed on each deployment.  
The scripts executed before the deployment are stored in the folder `data/apexscript/pre`.  
The scripts executed after the deployment are stored in the folder `data/apexscript/post`.

## File naming convention

1. Define a prefix within the stream (e.g. bp, sales, service, retail)
2. Number for order of execution
3. Short description: sprint number, user story number, what the script does

**Format:**

`<STREAM_PREFIX>_<NUMBER_FOR_ORDER_OF_EXECUTION>_<SHORT_DESCRIPTION>.apex`

**Examples:**

- `mpnl_19_sprint_12.2_US-15705_Delete_Home_to_Home_Authorisation.apex`
- `dfm_14_sprint026_US_15911_setup_marketing_cloud_info_order.apex`
- `Retail_10_Sprint_84_US-15007_add_roles_in_group.apex`

## Specific use cases

- Make changes in custom settings
- Add/Remove members of groups
- Change the role of users
- Add/Remove permission set assignments
- Perform DML operations on records 

## Few tips & tricks

- Make sure that your script will work in all environments by adding null checks
- Use unique identifiers for retrieving records
- Insert or Update (Upsert) with an external ID can reduce the number of DML statements in your code, and help you to avoid hitting governor limits.
- It is recommended to use upsert instead of insert so that, in case that the script is executed multiple times, no duplicates are created and the script will not fail.
- Group records in collections in order to minimize the number of DML statements.
- Before performing the DML operation, check for null/empty in order to reduce the number of DML statements.
---

[Home](/wiki/Home.md) - [Deployment](/wiki/deployment/deployment.md) - Anonymous apex scripts