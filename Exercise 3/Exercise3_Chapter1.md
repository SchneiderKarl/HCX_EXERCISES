# Chapter 1: Anonymize the Incident Report

< [Back to Exercise 3](./README.md)

## Table of contents

<!-- TOC -->

- [Chapter 1 - Exercise 3: Anonymize the Incident Report](#chapter-1---exercise-3-anonymize-the-incident-report)
  - [Table of contents](#table-of-contents)
  - [Create a new View](#create-a-new-view)
  - [Deploy to HANA Cloud](#deploy-to-hana-cloud)
  - [What you achieved in this chapter:](#what-you-achieved-in-this-chapter)

<!-- /TOC -->

## Create a new View

1. Switch back to BAS. Create a **New File** under the **View** folder and name it: ``V_INCIDENT_REPORT_ANONYMIZATION.hdbview``

   ![img](./Images/Exercise3_001.png)

2. Paste the code into the created file:
   ```
   VIEW "V_INCIDENT_REPORT_ANONYMIZATION" ("SEQUENCE", "SEX", "AGE", "OFFICE", "DIVISION", "INCIDENT_AMOUNT") AS
   SELECT "SEQUENCE", "SEX", "AGE", "OFFICE", "DIVISION", "INCIDENT_AMOUNT" 
   FROM "CV_INCIDENT_REPORT"  
   WITH ANONYMIZATION (ALGORITHM 'K-ANONYMITY' PARAMETERS '{"k": 2}' 
   COLUMN "SEQUENCE" PARAMETERS '{"is_sequence":true}' 
   COLUMN "SEX" PARAMETERS '{"is_quasi_identifier":true,"hierarchy":{"embedded":[["f"],["m"]]}}' 
   COLUMN "OFFICE" PARAMETERS '{"is_quasi_identifier":true,"min":1,"hierarchy":{"view":"V_OFFICE_HIERARCHY"}}' 
   COLUMN "AGE" PARAMETERS '{"is_quasi_identifier":true, "hierarchy":{"function":"F_GROUP_AGE", "levels":7}}' 
   COLUMN "DIVISION" PARAMETERS '{"is_quasi_identifier":true, "min":1,"hierarchy":{"embedded":[["Marketing","Customer Facing"],["Sales","Customer Facing"],["Development","Non Customer Facing"],["Research","Non Customer Facing"]]}}' 
   ) 
   ```
   It should look like this. 
   
   ![img](./Images/Exercise3_002.png)
   
   
## Deploy to HANA Cloud

**Deploy** the created view to HANA by clicking on the **rocket symbol**.


## What you achieved in this chapter:

- By executing the provided code snippet, you anonymize the Calculation View of your Incident Report using the integrated k-anonymity algorithm in HANA Cloud.
- If an attribute is a quasi-identifier, it will be anonymized using the predefined hierarchies or functions.
- K in the context defines the smallest possible group with the same quasi-identifiers.

![img](./Images/Exercise3_Progressbar1.png)

[Go to Chapter 2](./Exercise3_Chapter2.md) >
