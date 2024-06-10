# How to POC Tanzu Platform / Tanzu App Engine / Tanzu HUB 

Tanzu Platfom is the combination of several Tanzu products into one (Hub). 
This includes the former Tanzu Service Mesh (TSM) and Tanzu Mission Control (TMC).

This document will focus on how to get Tanzu Platform connected with an on-prem vCenter. 
Further how to get the "ole" nginx pod working. 

Assumption for this document is that vCenter is set up with Advanced Loadbalancer (AVI) or NSX-T (WCP enabled) 
A namespace has been created in vCenter. 

## Create a Cluster Group

```
Infrastructure -> Kubernetes Cluster -> Create Cluster Group
```
![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/ClGroup1.png)


## Register a TKG Instance (vCenter Supervisor cluster) 

```
Setup & Configuration -> Kubernetes Management -> Register TKG Instance 
```
![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/RegTKG1.png)

Use the from above created cluster group

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/RegTKG2.png)

This string will be pasted into the vCenter TMC window (See below) 

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/RegTKG3.png)


