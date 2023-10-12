# Understand the scenario

In this exercise,  you will develop a simple custom app (Online Shop) following ABAP Cloud development model. When the online shop entry is saved, a purchase requistion is created with the ordered item selected by the user. 
Assuming there is no released API available for purchase requisition, we will create a wrapper in Tier 2 (API Enablement layer) and release it for consumption in cloud. The online shop shall use the wrapper created in Tier 2 to post the purchase requisition.

    ![image](https://github.com/SAP-samples/teched2023-DT168/assets/102820487/ff23dc56-5c31-479e-8097-6cbbc11104e0)


<b>Note</b>:
The exercise follows the assumption that there is no suitable released API to create purchase requisitions, and we therefore need to find and wrap an unreleased API as a suitable alternative. Please be aware that we follow this assumption simply for illustrative purposes, as SAP does indeed provide a released API to create purchase requisitions (<a href="https://developers.sap.com/tutorials/abap-s4hanacloud-purchasereq-integrate-api.html">see Integrate released purchase requisition API into Online Shop Business Object</a>).                                                                        
Please note that the scenario has been developed for training purposes only and might not reflect all the complexity of a real-world scenario. The focus in these hands-on sessions is purely on technical knowledge transfer and therefore optimizations from a business perspective are not part of the training and the scenario will not be further assessed. 

## Result
You will have created an online shop entry which will post a purchase requisition using the wrapper over the not released BAPI.
<img width="935" alt="image" src="https://github.com/SAP-samples/teched2023-DT168/assets/102820487/3b42cc3f-1fd8-41d2-be83-e6682d17c295">

Continue to - [Exercise 1 - Implement wrapper for Purchase Requisition BAPI [BAPI_PR_CREATE](../ex1/README.md)
