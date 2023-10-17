# Exercise 3 - Enhance the Online Shop BO to post Purchase Requisition
When the user sets the status of the Online shop to P(Post), create Purchase Requisition using the wrapper created in Exercise 1

## [Exercise 3.1 Enhance the Behavior definition](#exercise-31-enhance-the-behavior-definition)
## [Exercise 3.2 Enhance the Metadata extension view](#exercise-32-enhance-the-metadata-extension-view)
## [Exercise 3.3 Enhance the Behavior implementation for validation and posting of the Purchase Requisition](exercise-33-enhance-the-behavior-implementation-for-validation-and-posting-of-the-purchase-requisition)
  

## Exercise 3.1 Enhance the Behavior definition

1. In the behavior definition, change the strict mode to strict(1). [**TODO** Reasoning]

```
managed implementation in class ZBP_R_ONLINESHOP_XXX unique;
strict ( 1 );
with draft;


2. Change the implementation to "Unmanaged Save" 

```
define behavior for ZR_ONLINESHOP_XXX alias OnlineShop
//persistent table zaonlineshop_801
draft table zdonlineshop_xxx
etag master LocalLastChangedAt
lock master total etag LastChangedAt
authorization master ( global )
with unmanaged save

3. Add save_modified method to the behavior implementation through quick assist. 


4. Add validation to check errors in purchase requisition

## Exercise 3.2 Enhance the Metadata extension view

1. Replace the code from ZC_ONLINESHOP_XXX with [this](../src/zc_onlineshop_xxx_mde.txt) code.

## Exercise 3.2 Enhance the Metadata extension view

## Exercise 3.3 Enhance the Behavior implementation for validation and posting of the Purchase Requisition
