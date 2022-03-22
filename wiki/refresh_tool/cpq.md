# CPQ refresh

---

CloudSense Products
The following CloudSense products are installed at PostNL:

	Configurator			The Product- & Pricing- model, and the ScreenFlows to perform CPQ
	Telco Sales Console		An improved UI for the CloudSense Product Basket
	Creator					The Terms & Conditions of a contract (Clauses and Sections)
	ClickApprove			Module to Send contract and let client sign via a Salesforce Site
	Order & Subscription	Generation of Subscriptions after an Opportunity is Closed – Won
	Orchestrator			Allows to define long-running processes (Visual Workflow)


To create a new Product for CPQ one should think of the following components in Salesforce/CloudSense:
1.	Product model: Commercial Product, Product, Commercial Product link
2.	Pricing model: Rate Card, Rate Card lines and optionally Discount Level and Product Reference
3.	Product Definition: ScreenFlows
4.	Offer: pre-filled Product Definition (a.k.a. the ‘initial Product Configuration’)
      The combination of the above allows an end-user to configure a Product end-to-end. To put this in context: an end-user will first select the Offer in the Product Basket. The offer can be seen as a pre-filled Product Definition. Within the Product Definition, amongst others, the references to Product and Commercial Product are retrieved based on Product Codes. Based on the Commercial Product Link selection the system or user can select the corresponding price components from the Pricing model.


CPQ is based on a significant amount of data (custom setting values, product definitions, offers and the full product and pricing data).

The data can be split into two ‘sections’:
1.	Product Definitions and Offers. Containing all related objects such as Attributes, Lookup, Screens, Categories, Definitions and so on.
2.	Reference Data referring to custom settings, product- & pricing data and other configuration

While performing a CPQ Refresh we upload these above mentioned data in the org.

There are Jenkins job performing these Refresh. To access these jobs go to
jenkins -> PostNL-Commercial-Factory -> Refresh [https://pipeline.drop.deloitte.nl/job/PostNL-Commercial-Factory/job/Refresh/]

Some of the jobs listed there are as follows:

CPQ Refresh for SALESTEST
CPQ Refresh to SALESDEV
CPQ Refresh to DASHTEST
CPQ Refresh to DFMTEST	etc.


[Before running the jenkins refresh job we have to make sure that the repository is updated with the recent files from Production.
There are two files.

Product Category(Including the product definitions):build/automated_ui_activities/prod_importfiles/SelectedCategories.json
Offer:build/automated_ui_activities/prod_importfiles/SelectedOffers.json

We have take export for the SelectedCategories.json and SelectedOffers.json from production and committ them by creating a pull request.]

These refresh jobs perform following tasks

1. CPQ Data Upsert Job

This job creates data for the following objects in the org:

CPQ_Discount_Group__c,cspmb__Price_Item__c,cspmb__Add_On_Price_Item__c,cspmb__Price_Item_Add_On_Price_Item_Association__c,CPQ_Service_Bundle_Link__c,cspmb__Discount_Level__c,cspmb__Rate_Card__c,cspmb__Rate_Card_Line__c,Product_Reference_Data__c,CPQ_NEA_Index__c,csbb__Configuration__c,csbb__Configuration_Association__c,CSPOFA__Orchestration_Process_Template__c,CSPOFA__Step_Class__c,CSPOFA__Orchestration_Step_Template__c,CSPOFA__Orchestration_Step_Dependency_Template__c,CSPOFA__Step_Class__c,CSPOFA__Orchestrator_Config__c,CSCAP__Click_Approve_Setting__c,cscfga__Json_Settings__c,csclmcb__CLM_Access_Options__c,csclmcb__CLM_Document_Generation_Settings__c,csclmcb__CLM_Options__c,CSPOFA__Compatibility_Settings__c,CSPOFA__Orchestrator_Constants__c,SKY_DropOut_Cases_Values__c,cscfga__CfgPkgConfig__c,cscfga__compatibility__c,CPQ_Settings__c,csexpimp1__CSOM_Impex_Config__c,csordtelcoa__Orders_Subscriptions_Options__c,csordtelcoa__Change_Types__c,CSCAP__ClickApprove_Document_Keywords__c,CSCAP__ClickApprove_Constants__c,CPQ_Hybris_Mapping__c,CPQ_Zone_mapping__c,CPQ_Service_level_mapping__c, csclm__Document_Definition__c,csclm__Document_Template__c,csclm__Document_Numbering_Setting__c,csclm__Section_Definition__c,csclm__Document_Template_Section_Association__c,csclm__Clause_Definition__c,csclm__Section_Clause_Definition_Association__c,csclm__Predicate__c,csclm__Applicability_Rule__c,csclm__Rule_Predicate_Association__c,CPQ_Contract_Translation_Paragraph__c,CPQ_Contract_Transl_DocTemp_Junction__c


2.  Runs the selenium script

It will import the Product Definitions and Offers. Containing all related objects such as Lookup, Screens, Categories, Definitions and so on. Compile all the product definitions.


---

[Home](/wiki/Home.md) - [Refresh tool](/wiki/refresh_tool/refresh_tool.md) - CPQ refresh
