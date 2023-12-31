# DT168 - Using ABAP Cloud to Build Extensions for SAP S/4HANA Cloud, Private Edition

## Description

This repository contains the material for the SAP TechEd 2022 session called DT168 - Using ABAP Cloud to Build Extensions for SAP S/4HANA Cloud, Private Edition.  

## Overview
In this Hands On Workshop, we will learn how to apply Cloud API Enablement Guidelines for SAP S/4HANA Cloud, private edition to consume an un released SAP API by adapting 3 tier extensibility model.

![](images/3-tier-1.png)


## Requirements

To carry out the exercises of this repository, you need to

Install the ABAP Development Tools (ADT) for ABAP development.
Have a browser ready, preferably Google Chrome, to see Fiori Elements preview.
Users for the development environment will be provided to you by the speakers/hosts during the session.

Go to Getting Started - Preparation to find out the installation details, URLs, then start with the first exercise.

## Exercises
- [Getting Started](exercises/ex0/)
- [Exercise 1 - Implement wrapper for Purchase Requisition BAPI BAPI_PR_CREATE](exercises/ex1/)
    - [Exercise 1.0 - Add Connection to ADT](exercises/ex1#exercise-10-create-package)
    - [Exercise 1.1 - Create Package Z_PURCHASE_REQ_TIER2_XXX](exercises/ex1#exercise-11-create-package)
    - [Exercise 1.2 - Create wrapper Interface ZIF_BAPI_PR_CREATE_XXX](exercises/ex1#exercise-12-create-interface-zif_bapi_pr_create_xx)
    - [Exercise 1.3 Create wrapper Class ZCL_WRAP_BAPI_PR_CREATE_XXX](exercises/ex1#exercise-12-create-wrapper-class-zcl_bapi_pr_wrapper_xx1)
    - [Exercise 1.4 - Create factory Class ZCL_BAPI_WRAP_FACTORY_XXX](exercises/ex1#exercise-12-create-factory-class-zcl_bapi_wrap_factory_xx)
    - [Exercise 1.5 - Release the Interface and Factory class](exercises/ex1#exercise-12-release-the-interface-and-factory-class)
- [Exercise 2 - Create Online Shop application](exercises/ex2/)
    - [Exercise 2.0 - Create Online Shop](exercises/ex2/README.md#exercise-20-create-online-shop)
    - [Exercise 2.1 - Enhance the Behaviour Implementation to generate Online Shop Order ID](exercises/ex2/README.md#exercise-21-enhance-the-behaviour-implementation-to-generate-online-shop-order-id-1)
    - [Exercise 2.2 - Enhance the Metadata extension view](exercises/ex2#exercise-22-enhance-the-metadata-extension-view-1)
    - [Exercise 2.3 - Test the Online Shop application](exercises/ex2#exercise-23-test-the-online-shop-application-1)
- [Exercise 3 - Integrate Wrapper for BAPI_PR_CREATE into Online Shop application](exercises/ex3/)
    - [Exercise 3.1 - Enhance the BO for validation and posting of the Purchase Requisition](exercises/ex3#exercise-31-enhance-the-bo-for-validation-and-posting-of-the-purchase-requisition-1)
    - [Exercise 3.2 - Test Online Shop with Purchase requistion creation](exercises/ex3#exercise-32-test-the-online-shop-application-1)  
  

**IMPORTANT**

Your repo must contain the .reuse and LICENSES folder and the License section below. DO NOT REMOVE the section or folders/files. Also, remove all unused template assets(images, folders, etc) from the exercises folder. 

## Contributing
Please read the [CONTRIBUTING.md](./CONTRIBUTING.md) to understand the contribution guidelines.

## Code of Conduct
Please read the [SAP Open Source Code of Conduct](https://github.com/SAP-samples/.github/blob/main/CODE_OF_CONDUCT.md).

## How to obtain support

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License
Copyright (c) 2023 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
