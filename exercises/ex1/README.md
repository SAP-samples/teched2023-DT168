# Exercise 1 - Implement wrapper for Purchase Requisition BAPI BAPI_PR_CREATE
In this exercise, we will create an interface to implement the wrapper class, the wrapper class and a factory class to instantiate the wrapper class. We will then release the interface and the factory class for Use in Cloud.
  
## [Exercise 1.1 Create Package $Z_PURCHASE_REQ_TIER2_XXX](#exercise-11-create-package) 
## [Exercise 1.2 Create wrapper Interface ZIF_BAPI_PR_WRAPPER_XXX](#exercise-12-create-wrapper-interface)
## [Exercise 1.3 Create wrapper Class ZCL_WRAP_BAPI_PR_CREATE_XXX](#exercise-13-create-wrapper-class)  
## [Exercise 1.4 Create factory Class ZCL_BAPI_WRAP_FACTORY_XXX](#exercise-14-create-factory-class)  
## [Exercise 1.5 Release Interface and Factory class](#exercise-15-release-interface-and-factory-class) 
## [Exercise 1.6 Run ATC and Request Exemptions](#exercise-16-run-atc-and-request-exemptions) 
## [Summary](#summary)


## Exercise 1.1 Create Package
1. In ADT, Goto **Project Explorer**. From the context menu of the ABAP Project, select **New -> ABAP Package**.
   &emsp;**Give the below information:**  
   &emsp;&emsp;**Name:** $Z_PURCHASE_REQ_TIER2_XXX  
   &emsp;&emsp;**Description**: Tier 2 for Purchase Requisition Wrapper  
   &emsp;&emsp;Select **Add to favorite package**  
   &emsp;&emsp;**Super Package**: $ZAPI_ENABLEMENT   
   &emsp;&emsp;**Package Type**: Development
   <br>
   <br>  
   &emsp;<img width="335" alt="image" src="https://github.com/SAP-samples/teched2023-DT168/assets/102820487/d7b2fee7-6556-4b31-8386-aaa018df1c24">
   
1. Press **Next** and verify the SWC is LOCAL
2. Press **Next** and **Finish**

## Exercise 1.2 Create wrapper Interface  
1. Select the package **$Z_PURCHASE_REQ_TIER2_XXX** and from the context menu, select **New -> ABAP Interface**.  
&emsp;**Give the below information:**  
&emsp;&emsp;**Name**: ZIF_BAPI_PR_WRAPPER_XXX  
&emsp;&emsp;**Description**: Wrapper Interface for BAPI_PR_CREATE  
<br>
<br>  
&emsp;&emsp;<img width="335" alt="image" src="https://github.com/SAP-samples/teched2023-DT168/assets/102820487/f7d54fd5-cf22-463b-95d7-186b7934c149">

2. Choose **Next** and **Finish**  
3. Insert the code from [here](../src/zif_bapi_pr_wrapper_xxx.txt) 
   
## Exercise 1.3 Create Wrapper Class   
1. Select the package **$Z_PURCHASE_REQ_TIER2_XXX** and from the context menu, select **New -> ABAP Class**.  
&emsp;**Give the below information:**  
&emsp;&emsp;**Name**: ZCL_WRAP_BAPI_PR_CREATE_XXX  
&emsp;&emsp;**Description**: Wrapper Class for BAPI_PR_CREATE   
<br>
<br> 
&emsp;&emsp;![image](https://github.com/SAP-samples/teched2023-DT168/assets/102820487/241e1453-aee9-4608-bcc7-9b31ed6ab4de)
  
&emsp;&emsp;Click on **Add..** and give the interface ZIF_BAPI_PR_WRAPPER_XXX created in previous step  
2. Choose **Next** and **Finish**  
3. Insert the code from [here](../src/zcl_wrap_bapi_pr_create_xxx.txt)
    
## Exercise 1.4 Create factory Class  
1. Select the package **$Z_PURCHASE_REQ_TIER2_XXX** and from the context menu, select **New -> ABAP Class**.  
&emsp;**Give the below information:**  
&emsp;&emsp;**Name**: ZCL_WRAP_BAPI_PR_CREATE_XXX  
&emsp;&emsp;**Description**: Wrapper Class for BAPI_PR_CREATE
<br>
<br> 
&emsp;&emsp;<img width="328" alt="image" src="https://github.com/SAP-samples/teched2023-DT168/assets/102820487/85100e91-acf4-4026-8a54-0e48221d4487">

2. Choose **Next** and **Finish**  
3. Insert the code from [here](../src/zcl_bapi_wrap_factory_xxx.txt)  
## Exercise 1.5 Release Interface and Wrapper Class       
## Exercise 1.6 Run ATC and Request Exemptions        
## Summary       
You've now created a Tier 2 wrapper on an unreleased BAPI and released for Use in Cloud.  
Continue to - [Exercise 2 - Create Online Shop application](../ex2/README.md)  
