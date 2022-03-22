# Platform Cache

---

#### What is platform cache?
Platform cache is a memory layer that stores session and org data in key-value pairs. When data is stored in memory, retrieving it
is a lot faster than doing queries.

#### Types of platform cache:
1. Org cache - stores data that anyone in the org can access across sessions, requests, users and profiles
2. Session cache - stores data for each individual user and is tied to that user's session

#### Use cases:
+ The navigation items in a community are stored in a custom object. When a new user enters the community, a query will be
  executed to retrieve the available navigation items. If these aren't changed very often(multiple times a day) and are not
  user-specific, they can be stored in the `org cache` so that the application will load faster considering it won't have to query
  the custom object again.
+ Users of your application have a set of products which they are allowed to use. As these are user-specific, they can be stored
  in the `session cache` so that when creating multiple orders, the allowed products are already stored in the cache and you don't
  have to query them again.

The implementation of platform cache is done in `App_PlatformCacheService`

`DOM_PlatformCache` is the domain layer of platform cache in which we store values of static/dynamic keys

#### How to use:
Let's say you want to create a method that retrieves the list of products which a user is authorized to use:
```
public List<String> retrieveAllowedProducts(String userId) {
    // Instantiate the cache service
    App_PlatformCacheService.IService cacheService = App_PlatformCacheService.newInstance();
    
    // Create the key which will be used to store/retrieve the data - in this use case, it should be unique per user
    String cacheKey = cacheService.makeSafeKey('ALLOWED_PRODUCTS:' + userId);
    
    // Try to retrieve the records
    List<String> allowedProducts = (List<String>) cacheService.get(cacheKey);
    
    // If allowedProducts is not null, it means that the records are available and we can return already
    if (allowedProducts != null) {
        return allowedProducts;
    } else {
        // allowedProducts was null, so we have to query
        allowedProducts = [SELECT Id, Name FROM Products WHERE User__c = :userId];
        // store the products in the cache so that subsequent calls can retrieve them from the memory directly
        cacheService.put(cacheKey, allowedProducts);
        return allowedProducts;
    }
}
```

Examples of using platform cache can be found in: `SAS_ParcelsProductsReadService`

---

[Home](/wiki/Home.md) - [Backend](/wiki/backend/backend.md) - Platform Cache
