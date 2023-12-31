# Exercise 2 - Create Online Shop application

In this exercise, we will create a custom application called Online Shop using ABAP Cloud Development model. The application creates an Online shop entry with the Ordered Item.

## [Exercise 2.0 Create Online Shop](#exercise-20-create-online-shop)
An empty online shop has been created for you already.This is for your reference ,please do not repeat steps `2.0.1-2.0.3`. 
<details> 
<summary>Click to expand!</summary>
   
**Exercise 2.0.1** Create Package
1. In ADT, Goto **Project Explorer**. From the context menu of the ABAP Project, select **New -> ABAP Package**.

   &emsp;**Give the below information:**
   
   &emsp;&emsp;**Name:** Z_ONLINESHOP_XXX  
   &emsp;&emsp;**Description**: Online Shop Application  
   &emsp;&emsp;Select **Add to favorite package**  
   &emsp;&emsp;**Super Package**: ZLOCAL   
   &emsp;&emsp;**Package Type**: Development
   <br>
   <br>    
   ![](images/Create_Package_Ex2.jpg)
   <br>
1. Press **Next** and verify the SWC is LOCAL
2. Press **Next**, Choose TR HE4K917701 and **Finish**
![](images/TR.jpg)

**Exercise 2.0.2** Create database table
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
     @Semantics.amount.currencyCode : 'zaonlineshop_xxx.currency'
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

**Exercise 2.0.3** Generate Transactional UI Service
1. Select the table created **zaonlineshop_xxx** and from context menu, choose **Generate ABAP Repository Objects**. Select **ABAP RESTful Application Programming Model: UI Service**

![](images/Gen_Repo1.jpg) 

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
   Press **Next**  
3. Review the names of the repository objects that are going to be generated and Press **Next**

![](images/Gen_Repo2.jpg) 

   Choose the transport request HE4K917701 and press **Finish**

   
5. **Publish** the Service Binding ZUI_V4_ONLINESHOP_XXX


</details> 

**Exercise 2.0.4** Enhance the BO to add Purchase Requisition details 

1. Add fields for Order ID, Purchase Requisition and Purchase Requistion creation date to list of read only fields and add determination to generate the Online Shop Order ID. The modified code should look like below:

   ```
   managed implementation in class ZBP_R_ONLINESHOP_XXX unique;
   strict ( 2 );
   with draft;
   
   define behavior for ZR_ONLINESHOP_XXX alias OnlineShop
   persistent table zaonlineshop_xxx
   draft table zdonlineshop_xxx
   etag master LocalLastChangedAt
   lock master total etag LastChangedAt
   authorization master ( global )
   
   {
     field ( readonly )
     OrderID,
     PurchaseRequisition,
     PurchRqnCreationDate,
     CreatedBy,
     CreatedAt,
     LastChangedBy,
     LastChangedAt,
     LocalLastChangedAt;
   
     field ( numbering : managed )
     OrderUUID;
   
     create;
     update;
     delete;
   
     determination CalculateOrderID on save { create; }
   
     draft action Edit;
     draft action Activate;
     draft action Discard;
     draft action Resume;
     draft determine action Prepare;
   
     mapping for ZAONLINESHOP_xxx
     {
       OrderUUID = ORDER_UUID;
       OrderID = ORDER_ID;
       OrderItemID = ORDER_ITEM_ID;
       OrderItemPrice = ORDER_ITEM_PRICE;
       OrderItemQuantity = ORDER_ITEM_QUANTITY;
       Currency = CURRENCY;
       OverallStatusIndicator = OVERALL_STATUS_INDICATOR;
       DeliveryDate = DELIVERY_DATE;
       Notes = NOTES;
       PurchaseRequisition = PURCHASE_REQUISITION;
       PurchRqnCreationDate = PURCH_RQN_CREATION_DATE;
       CreatedBy = CREATED_BY;
       CreatedAt = CREATED_AT;
       LastChangedBy = LAST_CHANGED_BY;
       LastChangedAt = LAST_CHANGED_AT;
       LocalLastChangedAt = LOCAL_LAST_CHANGED_AT;
     }
   }
1. Press **Ctrl+1** on the added determination CalculateOrderID to load the quickassist. Select the promt to add corresponding method to the behavior implementation.

![](images/QuickAssist.jpg)  

## [Exercise 2.1 Enhance the Behaviour Implementation to generate Online Shop Order ID](#exercise-21-enhance-the-behaviour-implementation-to-generate-online-shop-order-id)  

## [Exercise 2.2 Enhance the Metadata extension view](#exercise-22-enhance-the-metadata-extension-view-1)  

## [Exercise 2.3 Test the Online Shop application](#exercise-23-test-the-online-shop-application-1)  

## [Summary](#summary-1)


    
## Exercise 2.1 Enhance the Behaviour Implementation to generate Online Shop Order ID

1. Add the below code to calculateOrderID method of class ZBP_R_ONLINESHOP_XXX   

   ```
   METHOD CalculateOrderID.

    READ ENTITIES OF zr_onlineshop_XXX IN LOCAL MODE
      ENTITY OnlineShop
        FIELDS ( OrderID )
        WITH CORRESPONDING #( keys )
      RESULT DATA(OnlineOrders).

    SELECT MAX( order_id ) FROM zaonlineshop_XX INTO @DATA(max_order_id). "active table
    SELECT SINGLE FROM zdonlineshop_XXX FIELDS MAX( orderid ) INTO @DATA(max_orderid_draft). "draft table
    IF max_orderid_draft > max_order_id.
      max_order_id = max_orderid_draft.
    ENDIF.

    "set initial values of new instances
    MODIFY ENTITIES OF zr_onlineshop_XXX IN LOCAL MODE
      ENTITY OnlineShop
        UPDATE FIELDS ( OrderID )
        WITH VALUE #( FOR order IN OnlineOrders INDEX INTO i (
                          %tky          = order-%tky
                          OrderID       = max_order_id + i
                        ) ).
     ENDMETHOD.
   
## Exercise 2.2 Enhance the Metadata extension view
1. Replace the code from Metadata extension ZC_ONLINESHOP_XXX with [this](../src/zc_onlineshop_xxx.txt) code.
   
## Exercise 2.3 Test the Online Shop application
1. Go to the Service binding ZUI_ONLINESHOP_O4_XXX, select the entity **OnlineShop** and **Preview**  
2. Test the application
## Summary
You've now created an Online Shop application. Now let us integrate this application with Purchase Requisition.
Continue to - [Exercise 3 - Post Purchase Requisition using Tier 2 wrapper ](../ex3/README.MD)
