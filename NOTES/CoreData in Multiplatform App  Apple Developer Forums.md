Hi I have an issue with Multiplatform app which use CoreData Hosted in CloudKit

Xcode 12 Beta 5 (12A8189h)

I don't change anything in the code and try to run it.

Build succeed

Run the app on macOs and get immediately this crash

```
Code Block 2020-08-22 09:08:36.342795+0200 Testing[27537:463165] [error] error:  Failed to load model named TestingCoreData: error:  Failed to load model named Testing2020-08-22 09:08:36.421964+0200 Testing[27537:463165] [error] error: No NSEntityDescriptions in any model claim the NSManagedObject subclass 'Item' so +entity is confused.  Have you loaded your NSManagedObjectModel yet ?CoreData: error: No NSEntityDescriptions in any model claim the NSManagedObject subclass 'Item' so +entity is confused.  Have you loaded your NSManagedObjectModel yet ?2020-08-22 09:08:36.422022+0200 Testing[27537:463165] [error] error: +[Item entity] Failed to find a unique match for an NSEntityDescription to a managed object subclassCoreData: error: +[Item entity] Failed to find a unique match for an NSEntityDescription to a managed object subclassFatal error: UnsafeRawBufferPointer with negative count: file Swift/UnsafeRawBufferPointer.swift, line 8722020-08-22 09:08:36.553889+0200 Testing[27537:463165] Fatal error: UnsafeRawBufferPointer with negative count: file Swift/UnsafeRawBufferPointer.swift, line 872
```

Run it on iOS iPhone 11 Pro and get imidiatly crash

```
Code Block 2020-08-22 09:09:55.269931+0200 Testing[27619:465943] [error] error:  Failed to load model named TestingCoreData: error:  Failed to load model named Testing2020-08-22 09:09:55.317706+0200 Testing[27619:466516] libMobileGestalt MobileGestaltCache.c:38: No persisted cache on this platform.2020-08-22 09:09:55.334598+0200 Testing[27619:465943] [error] error: No NSEntityDescriptions in any model claim the NSManagedObject subclass 'Item' so +entity is confused.  Have you loaded your NSManagedObjectModel yet ?CoreData: error: No NSEntityDescriptions in any model claim the NSManagedObject subclass 'Item' so +entity is confused.  Have you loaded your NSManagedObjectModel yet ?2020-08-22 09:09:55.334797+0200 Testing[27619:465943] [error] error: +[Item entity] Failed to find a unique match for an NSEntityDescription to a managed object subclassCoreData: error: +[Item entity] Failed to find a unique match for an NSEntityDescription to a managed object subclassFatal error: UnsafeRawBufferPointer with negative count: file Swift/UnsafeRawBufferPointer.swift, line 8722020-08-22 09:09:55.370937+0200 Testing[27619:465943] Fatal error: UnsafeRawBufferPointer with negative count: file Swift/UnsafeRawBufferPointer.swift, line 872
```

In Xcdatamodelid there is nothing to pick from Class -> Module (in previous versions was Current Module as an option there)

-   Tried to clean derived data
-   Tried to clean project
-   Tried to change Item Class module from Global namespace to hardly written Current Module
-   Tried to change Codegen from ClassDefinition to Manual / None and create property my self