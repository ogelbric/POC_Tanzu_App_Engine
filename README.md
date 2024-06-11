# How to POC Tanzu Platform / Tanzu App Engine / Tanzu HUB 

Tanzu Platfom is the combination of several Tanzu products into one (Hub). 
This includes the former Tanzu Service Mesh (TSM) and Tanzu Mission Control (TMC) and more...

This document will focus on how to get Tanzu Platform connected with an on-prem vCenter and 
how to get the "ole" nginx pod working (i.e. Random cutomer application). 

Assumption for this document is that vCenter is set up with Advanced Loadbalancer (AVI) or NSX-T (WCP enabled) 
A namespace has been created in vCenter (with everything in working order in the namespace). 

## Select the VMware Tanzu Platform Tile from the Cloud Console

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/tanzuplatform1.png)


## (1) Create a Cluster Group

```
Infrastructure -> Kubernetes Cluster -> Create Cluster Group
```
![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/ClGroup1.png)


## (2) Register a TKG Instance (vCenter Supervisor cluster) 

```
Setup & Configuration -> Kubernetes Management -> Register TKG Instance 
```
![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/RegTKG1.png)

Use the from above created cluster group

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/RegTKG2.png)

This string will be pasted into the vCenter TMC window (See below) 

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/RegTKG3.png)

In this case the string / vCenter is already enabled
Note: A vCenter Supervisor cluster can only talk to TMC or to App Enginge right now. Disconnect TMC before connecting Tanzu Platoform

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/vSphereTMCWindow1.png)

## (3) Create a workload cluster 

```
Infrastructure -> Kubernetes Cluster -> Add Cluster
```

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/CC1.png)

Create Tanzu Kuberenetes Grid Cluster

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/CC2.png)

Select Supervisor Cluster and Namespace

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/CC3.png)

Decide on cluster name a use Cluster Group created earlier and most important Step
Label The Cluster (somthing better then in my case mycluster) !!!

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/CC4.png)

Decide on OS and storage policy

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/CC5.png)

Decide on node size and storage policy

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/CC6.png)

Untouched

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/CC7.png)

Decide on node size and how many

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/CC8.png)

Result
(Notice the label) 
![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/CC9.png)





# Tips and tricks
# Space enablement turns yellow
In my case the cause was that the capabilities in the space and in the cluster group did not match. 

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/kirtiyellowspace.png)

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/kirticapabilitiesclustergroupandspace.png)



