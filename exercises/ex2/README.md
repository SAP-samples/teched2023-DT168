# Exercise 2 - Create Online Shop application

In this exercise, we will create a custom application called Online Shop using ABAP Cloud Development model. The application creates an Online shop entry with the Ordered Item.

> An empty online shop has been created for you already. So, skip to Exercise 2.4

## [Exercise 2.1 Create Package Z_ONLINE_SHOP_XXX](#exercise-21-create-package) 

## [Exercise 2.2 Create database table ZAONLINESHOP_XXX](#exercise-22-create-database-table) 

## [Exercise 2.3 Generate Transactional UI Service](#exercise-23-generate-transactional-ui-service)

## [Exercise 2.4 Enhance the BO to generate Online Shop Order ID](#exercise-24-enhance-the-bo-to-generate-online-shop-order-id)  

## [Exercise 2.5 Test the Online Shop application](#exercise-25-test-the-online-shop-application)

## [Summary](#summary)



## Exercise 2.1 Create Package
1. In ADT, Goto **Project Explorer**. From the context menu of the ABAP Project, select **New -> ABAP Package**.

   &emsp;**Give the below information:**
   
   &emsp;&emsp;**Name:** Z_ONLINESHOP_XXX  
   &emsp;&emsp;**Description**: Tier 2 for Purchase Requisition Wrapper  
   &emsp;&emsp;Select **Add to favorite package**  
   &emsp;&emsp;**Super Package**: $ZLOCAL   
   &emsp;&emsp;**Package Type**: Development
   <br>
   <br>    
   &emsp;<img width="335" alt="image" src="https://github.com/SAP-samples/teched2023-DT168/assets/106324991/da9e7a02-769d-4e16-bd5e-6a49fc99af59">
   <br>
1. Press **Next** and verify the SWC is LOCAL
2. Press **Next** and **Finish**

## Exercise 2.2 Create database table
1. From the context menu of the package **Z_ONLINESHOP_XXX**, choose **New** --> **Other Repository Object**, search for 'database table' and enter the following information:  
&emsp;&emsp;i. **Name**: zaonlineshop_xxx  
&emsp;&emsp;ii.**Description**: Online Shop data  
&emsp;&emsp;iii. Press **Next** and select the transport request and choose **Finish**  
2. Enter the below code and activate
   
   ```
   @EndUserText.label : 'Online Shop'
   @AbapCatalog.enhancement.category : #NOT_EXTENSIBLE
   @AbapCatalog.tableCategory : #TRANSPARENT
   @AbapCatalog.deliveryClass : #A
   @AbapCatalog.dataMaintenance : #NOT_ALLOWED
   define table zaonlineshop_xxx {
     key client               : mandt not null;
     key order_uuid           : sysuuid_x16 not null;
     order_id                 : abap.char(10);
     order_item_id            : abap.char(40);
     @Semantics.amount.currencyCode : 'zaonlineshop_801.currency'
     order_item_price         : abap.curr(11,2);
     order_item_quantity      : abap.numc(4);
     currency                 : abap.cuky;
     overall_status_indicator : zos_status;
     delivery_date            : abap.dats;
     notes                    : abap.string(256);
     purchase_requisition     : abap.char(20);
     purch_rqn_creation_date  : abap.dats;
     created_by               : abp_creation_user;
     created_at               : abp_creation_tstmpl;
     last_changed_by          : abp_lastchange_user;
     last_changed_at          : abp_lastchange_tstmpl;
     local_last_changed_at    : abp_locinst_lastchange_tstmpl;
   }

## Exercise 2.3 Generate Transactional UI Service  
1. Select the table created **zaonlineshop_xxx** and from context menu, choose **Generate ABAP Repository Objects**. Select **ABAP RESTful Application Programming Model: UI Service**

   <img width="353" alt="image" src="https://github.com/SAP-samples/teched2023-DT168/assets/102820487/cb3b4526-a1eb-4b8f-858d-47c48e28ec69">  

2. Give the below information in the wizard:
     i. **Data Model**:  
     &emsp;&emsp;**Data Definition Name**: ZR_ONLINESHOP_XXX  
     &emsp;&emsp;**Alias Name**: OnlineShop  
     ii. **Behavior**:  
     &emsp;&emsp;**Implementation Class**: ZBP_R_ONLINESHOP_XXX  
     &emsp;&emsp;**Draft Table Name**: ZDONLINESHOP_XXX  
     iii.**Service Projection**: ZC_ONLINESHOP_XXX  
     iv. **Business Service**:  
     &emsp;&emsp;**Service Definition**: ZUI_ONLINESHOP_XXX  
     &emsp;&emsp;**Service Binding**: ZUI_V4_ONLINESHOP_XXX  
         
## Exercise 2.4 Enhance the BO to generate Online Shop Order ID  
1. Add 
## Exercise 2.5 Test the Online Shop application  
## Summary
You've now created an Online Shop application. Now let us integrate this application with Purchase Requisition.
Continue to - [Exercise 3 - Post Purchase Requisition using Tier 2 wrapper ](../ex3/README.md)
