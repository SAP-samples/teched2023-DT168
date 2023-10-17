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
  ```

2. Change the implementation to "Unmanaged Save" 

  ```
  define behavior for ZR_ONLINESHOP_XXX alias OnlineShop
  //persistent table zaonlineshop_801
  draft table zdonlineshop_xxx
  etag master LocalLastChangedAt
  lock master total etag LastChangedAt
  authorization master ( global )
  with unmanaged save  
  ```
3. Add validation to check errors in purchase requisition

i. Add validation to the Behavior definition

```
  create;
  update;
  delete;

  validation checkPurchaseRequisition on save {create;}
  determination CalculateOrderID on save { create; }
```

```
  //  draft determine action Prepare;
  draft determine action Prepare { validation checkPurchaseRequisition; }
```

4. Add save_modified method to the behavior implementation through quick assist and add the code as below:

```
    DATA lr_descr_struc TYPE REF TO data.
    DATA lo_structdescr TYPE REF TO cl_abap_structdescr.
    DATA r_online_shop_old TYPE zr_onlineshop_XXX.
    IF create-onlineshop IS NOT INITIAL.
      online_shop = CORRESPONDING #( create-onlineshop MAPPING FROM ENTITY ).
    ENDIF. 
    IF update-onlineshop IS NOT INITIAL.
      SELECT * FROM zaonlineshop_XXX
             FOR ALL ENTRIES IN @update-onlineshop
             WHERE order_uuid = @update-onlineshop-OrderUUID
             INTO TABLE @DATA(online_shop_old_t).

      CREATE DATA lr_descr_struc TYPE zr_onlineshop_XXX. " <- any type
      lo_structdescr ?= cl_abap_structdescr=>describe_by_data_ref( p_data_ref = lr_descr_struc ).
      LOOP AT update-onlineshop ASSIGNING FIELD-SYMBOL(<onlineshop_new>).
        DATA(online_shop_old) = online_shop_old_t[ order_uuid = <onlineshop_new>-OrderUUID ].
        r_online_shop_old = CORRESPONDING #( online_shop_old MAPPING TO ENTITY ).
        LOOP AT lo_structdescr->components ASSIGNING FIELD-SYMBOL(<comp>).
          ASSIGN COMPONENT <comp>-name OF STRUCTURE <onlineshop_new>-%control TO FIELD-SYMBOL(<fld_cntrl>).
          IF <fld_cntrl> IS ASSIGNED AND <fld_cntrl> = '01'.
            ASSIGN COMPONENT <comp>-name OF STRUCTURE <onlineshop_new> TO FIELD-SYMBOL(<new_value>).
            ASSIGN COMPONENT <comp>-name OF STRUCTURE r_online_shop_old TO FIELD-SYMBOL(<old_value>).
            <old_value> = <new_value>.
          ENDIF.
        ENDLOOP.
        APPEND CORRESPONDING #( r_online_shop_old MAPPING FROM ENTITY ) TO online_shop.
      ENDLOOP.
    ENDIF.

    LOOP AT online_shop ASSIGNING FIELD-SYMBOL(<online_shop>) WHERE overall_status_indicator = zbp_r_onlineshop_XXX=>c_overall_status-post.
      DATA pr_returns TYPE zif_wrap_bapi_pr_create_xx=>pr_returns.
      <online_shop>-purchase_requisition = zcl_bapi_wrap_factory_xx=>create_instance( )->create(
        EXPORTING
          pr_header        = VALUE zif_wrap_bapi_pr_create_xx=>pr_header( pr_type = 'NB' )
          pr_items         = VALUE zif_wrap_bapi_pr_create_xx=>pr_items( (
            preq_item  = '00010'
            plant      = '1710'
            acctasscat = 'U'
            currency   = <online_shop>-Currency
            deliv_date = <online_shop>-Delivery_Date
            material   = <online_shop>-order_item_id
            matl_group = 'L001'
            preq_price = <online_shop>-order_item_price
            quantity   = <online_shop>-order_item_quantity
            unit       = 'EA'
            pur_group = '001'
            purch_org = '1010'
            short_text = <online_shop>-notes
          ) )
        IMPORTING
          pr_returns    = pr_returns
      ).

      ASSERT NOT line_exists( pr_returns[ type = 'E' ] ).
      <online_shop>-purch_rqn_creation_date = cl_abap_context_info=>get_system_date(  ).
      <online_shop>-overall_status_indicator = zbp_r_onlineshop_XXX=>c_overall_status-submitted.
    ENDLOOP.

    MODIFY zaonlineshop_XXX FROM TABLE @online_shop.

    LOOP AT delete-onlineshop INTO DATA(onlineshop_delete) WHERE OrderUUID IS NOT INITIAL.
      DELETE FROM zaonlineshop_XXX WHERE order_uuid = @onlineshop_delete-OrderUUID.
      DELETE FROM zdonlineshop_XXX WHERE orderuuid = @onlineshop_delete-OrderUUID.
    ENDLOOP.

  ENDMETHOD.

  ```


## Exercise 3.2 Enhance the Metadata extension view

1. Replace the code from ZC_ONLINESHOP_XXX with [this](../src/zc_onlineshop_xxx_mde.txt) code.

## Exercise 3.2 Enhance the Metadata extension view

## Exercise 3.3 Enhance the Behavior implementation for validation and posting of the Purchase Requisition
