# FFLIB - service, selector, domain layers, mapping metadata

---

"`Enterprise Design Patterns` consists of different layers in our applications working together following design principles 
to enable our applications to scale''

`Layers` are introduced, each with their own ‘concern’ and ‘responsibility’, which makes the code easy to understand thanks 
to the well-structured context and purpose.

Layers involved in Enterprise Design Patterns:

- Domains: Containing all data manipulation for one object (incl. trigger handlers and statics)
- Selectors: Containing all SOQL queries for one object
- Services: Containing all logic for one specific (business) process
- Unit of Work: ‘Working layer’ gathering all DML actions and orchestrating moment of commit
    
### Naming conventions:

- `Domain`:  
    - Prefix: DOM_
    - Example: DOM_Accounts
    - Comments: plural names to indicate layer is bulkified

            
- `Selector`:   
    - Prefix: SEL_
    - Example: SEL_Accounts
    - Comments: plural names to indicate layer is bulkified
            
            
- `Service`:    
    - Prefix: XX_YYY_Service
    - Example: PNP_SendNotificationsToMC_Service.cls
    - Comments: service classes can have as a prefix as an identifier for the functional group they are part of, 
followed by a name that represents the business process implemented and must end with the key-word 'Service'


### Service Layer - Business Logic Specific 

This is the business logic layer in the application. It’s called by different execution contexts or entry points like
Apex UI Controller, Apex Web Service, Apex REST Service, Invocable Method, Inbound Email Handler, Batch APEX, Schedule APEX, 
Queueable etc. Service classes should be called agnostic - callable from anywhere in the system and should always be 
designed for bulk processes.

Services can call other services, domains or even selectors directly. When calling other services they are referred to 
as compound services.

[Learn more about Service layer](https://quirkyapex.com/2016/09/03/fflib-service-layer/)

### Selector Layer - Object Specific

This is layer in the application is only responsible for running queries, the main benefits being maximizing
query reusability and reducing duplicates in the code base.

Security checks are also performed in this layer to ensure correct access to the data.

It allows selecting a common set of fields which can be used across the application, which reduces the risk of fields 
not selected, when the query result is later processed.

In the initialization statement below, the parameters are, in order: assertCRUD, enforceFLS, includeSelectorFields:
```
fflib_QueryFactory factory = newQueryFactory(false, false, true);
```
[Learn more about Selector layer](https://quirkyapex.com/2016/08/18/fflib-selector-layer/)


### Domain Layer - Object Specific

This is the trigger handler layer in the application, directly invoked from the trigger context.

Domain Layer has to be object specific and it's the go-to-place for object related methods and statics.

Domains can be initialized outside of a trigger context and populated with a list of records.

All functionality within the domain layer must be bulkified.

[Learn more about Domain layer](https://quirkyapex.com/2016/08/16/fflib-domain-layer/)

### Unit of Work – Transaction management

UOW pattern is an approach to centralise all database activities into a single wrapper class for transaction 
management, populating of lookup fields automatically and allowing developers to safely commit the work without disrupting 
other layers within the application, whilst also removing duplication throughout the whole code base by removing repetitive 
boiler plate code.

Benefits:

- Determine Order of SObjects (see Application class)
- Populating relationship fields: a very common scenario is the need of referencing the newly created parent id, when 
inserting the child records

```
       public PageReference save(){
           // Create the account and insert it immediately
           // so we can get the ID of the record
           Account a = new Account(Name = 'Quirky Apex');
           insert a;
            
           // Create the contacts and link it to the account
           List<Contact> contacts = new List<Contact>();
         
           for(Integer i=0; i < 10; i++){
              Contact contact = new Contact(
                 LastName = 'QA' + i,
                 AccountId = a.Id
              );
              contacts.add(contact);
           }
            
           // Insert all of the contacts
           insert contacts;
         
           return null;
        }
```
    
- Transaction Management: UOW aggregates DML operations and wraps them in a SavePoint when the commitWork method is called
- Uncommitted work exceptions: These exceptions can be avoided by passing the UOW instance around in the application and 
calling the commitWork method at a safe point.
```
public PageReference save(){
   // Set up the unit of work
   fflib_ISObjectUnitOfWork uow = new fflib_SObjectUnitOfWork(
      new List<Schema.SObjectType>{
         Log__c.sObjectType
      }
   );
    
   // Make a callout and pass the instance of the uow
   MyCalloutClass.doCallout(uow);
   AnotherCalloutClass.doCallout(uow);
    
   // Commit all of the work at a safe moment
   uow.commitWork();
}
```
- Automatically handling bulkification by staging records and perform DML at the end of transaction

[Learn more about UOW](https://quirkyapex.com/2016/08/21/fflib-unit-of-work/)


### Application class: App_Application.cls

The “Application class” resides at the heart of the codebase.
It contains the order by which SObjects should be saved to the database (i.e. Account first, then a child Contact, then 
a child Case)
```
public static final fflib_Application.UnitOfWorkFactory unitOfWork = new fflib_Application.UnitOfWorkFactory(
			new List<SObjectType> {
					Account.sObjectType,
					Contact.sObjectType,
					Case.sObjectType,
			}
	);
```

It is responsible for defining the classes that will handle different types of business logic requests within the code base. 
For example, for the Account SObject we can define which selector to use or for the Contact SObject  which domain class to use.

This has been recently refactored to make use of Custom Metadatas for storing the mapping between the Implementation Type
and the SObject/Interface type. Therefore, whenever a new Service/Domain/Selector class is introduced, a record has to be 
created in the corresponding Custom Metadata:

- FFLIB_Service_Mapping__mdt
- FFLIB_Domain_Mapping__mdt
- FFLIB_Selector_Mapping__mdt

	
---

[Home](/wiki/Home.md) - [Coding best practices](/wiki/coding_best_practices/coding_best_practices.md) - FFLIB - service, selector, domain layers, mapping metadata
