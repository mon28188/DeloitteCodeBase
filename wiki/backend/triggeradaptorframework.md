# Trigger adaptor framework

---

Triggers enable you to perform custom actions before or after changes to Salesforce records,
such as insertions, updates, or deletions.

As per the Salesforce best practices, there should only be one trigger per SObject.
Inside the trigger, the corresponding DOM class will be directly invoked, where the trigger orchestration will take place.

```
trigger CasesTrigger on Case (after insert, after delete, after undelete) {
    if(UT_Triggers.isEnabled(Case.sObjectType)){
        fflib_SObjectDomain.triggerHandler(DOM_Cases.class);
    }
}
```
All domain layers have to extend `fflib_SObjectDomain`.

```
public with sharing class DOM_Cases extends fflib_SObjectDomain implements IDomain {

}
```

In order to create a trigger handler, the `DOM_` class should call the `registerHandler` method.
Domain layers should call this method to register a handler which should be fired in a trigger context.
This should be called from within the domain layers constructor.

```
public DOM_Cases(List<Case> cases){
        super(cases, App_Application.unitOfWork.newInstance());

        registerHandler(TriggerEvent.BEFORE_INSERT, UpdateCaseWithEntitlement.class);
    }
```
RegisterHandler method parameters, in order:
* @param tEvent             Trigger event which should be registered for the handler.
* @param handlerType        The class type of the handler which will be used to instantiate the class.

### Types of trigger event
- BEFORE_INSERT
- BEFORE_UPDATE
- BEFORE_DELETE
- AFTER_INSERT
- AFTER_UPDATE
- AFTER_DELETE
- AFTER_UNDELETE
- ALL

The class mentioned in the `registerHandler` should be created as inner class inside the domain layer. It should extend `BaseHandler`
and also implement different interfaces depending on the behaviour of the trigger handler when called multiple times within the
same transaction and also the TriggerEvents that it should run for.

```
public with sharing class UpdateCaseWithEntitlement extends BaseHandler implements FireOnce, BeforeInsert, BeforeUpdate {

}
```

### Interfaces

`FireOnce` - Handlers should implement this interface if they wish to use the functionality
whereby the handlers are only fired once per record.

`FireOnceCombined` - After insert and update events are the slowest events to handle.
For trigger handlers which implement this interface the after update will not
fire if the after insert event returned true for being processed. This is to avoid
rerunning logic unnecessarily.

```
public interface FireOnceCombined {}
```

`BeforeInsert`, `BeforeUpdate`, `BeforeDelete`, `AfterInsert`, `AfterUpdate`, `AfterDelete`,
`AfterUndelete`, `AllEvents` - Interface which should be implemented by trigger handlers
to indicate which trigger event they are listening for.



Once extended, `BaseHandler` has 3 methods that can be overridden:

- `initialize` - Initialize phase of the trigger handler.

```
public override void initialize( TriggerState ts, fflib_ISObjectUnitOfWork uow ) {
    patterns = SEL_SKYBarcodeRegex.newInstance().selectAllActivePatterns();
}
```
- `process` - Processes a single record within a trigger context. This method gets executed for
  each record. This is why this method should not contain DML operations, queries.

```
public override Boolean process( SObject current, SObject original, fflib_ISObjectUnitOfWork uow ) {
    Case newRecord = (Case) current;
    Case oldRecord = (Case) original;
    Boolean isProcessed =  false;
    if(condition){
        isProcessed = true;
    }
    return isProcessed;
}
```
- `finalize` - Finalize phase of the trigger handler.

```
public override void finalize(TriggerState state, fflib_ISObjectUnitOfWork uow) {
    if( !incomingEmailsIds.isEmpty() ){
        uow.commitWork();
    }
}
```

A instance of the `TriggerState` class will be injected into the initialize and finalize phases of every trigger handler. It
allows the trigger handler to preload or bulk perform actions.

---

[Home](/wiki/Home.md) - [Backend](/wiki/backend/backend.md) - Trigger adaptor framework
