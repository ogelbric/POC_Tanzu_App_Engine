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

## (4) Install into the Cluster Group Capabilities

```
Application Spaces -> Capabilities -> Avaliable -> Select -> Install
```

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/cgcap1.png)

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/cgcap2.png)

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/cgcap3.png)

## (5) Create a Profile

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/prof1.png)

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/prof2.png)

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/prof3.png)

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/prof4.png)

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/prof5.png)

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/prof6.png)

## (6) Create an Availability Target

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/at1.png)

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/at2.png)

Here comes my ill choosen cluster label into play

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/at3.png)


## (7) Create a Space

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/sp1.png)

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/sp2.png)

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/sp3.png)

## (8) Create my first simple app (Follow link)

[My First Simple App](https://github.com/ogelbric/POC_Tanzu_App_Engine_app1/blob/main/README.md)

# Tips and Tricks

# Tanzu login (was not obvious to me...) 

```
When a tanzu login is used a URL is being displayd which needs to be pasted into a browser
```
![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/tlogin1.png)

```
The result is a strange screen from which the token for the "password" answer has to be used
```
![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/tlogin2.png)

# The other way to log in is via sourcing a file

The org ID is in the GUI Console (upper right hand corner and the API token is under User Settings My Account)

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/org1.png)

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/tok1.png)

```
cat tanzucli.src
export TANZU_CLI_CLOUD_SERVICES_ORGANIZATION_ID=77aee83b-308f-BBBB-AAAA-3xxxxxxxxx5
export TANZU_CLI_OAUTH_LOCAL_LISTENER_PORT=9090
export TANZU_API_TOKEN=_fGOgUtC-sazFVgfjgdGakxLxV_your_token_here_Z5xVWJGUO1T9vfJEej-fOU
```
# Study in api-resources in various stages with in the tanzu cli
In the tanzu cli the context is the key to be able to do certain things.
Hence the different api-resources available at different stages
The stages I looked at are:
Login
Project
Cluster Group
Space

Please adjust in the script the variables for your environment 
(Further I have the API token in a file)

```
source tanzucli.src
export proj="AMER-East"
export sp="orfspace1"
export org="sa-tanzu-platform"
export cl="orfclustergroup"
export w=''
#export w='--wide'
#
#Results in 23 api-resources - just loggin in
#
yes | tanzu context delete $org
source ./tanzucli.src
tanzu login
tanzu context list $w
k api-resources | wc -l
#
#Results in 29 api-resources - setting the Project
#
tanzu project use $proj
tanzu context list  $w
k api-resources | wc -l
#
#Results in 27 api-resources - setting the cluster group
#
tanzu operations clustergroup use  $cl
tanzu context list  $w
k api-resources | wc -l
#
#
#Results in 20 api-resources - setting the space
#
tanzu space use $sp 
k api-resources | wc -l
tanzu context list  $w
#
#Results in 23 api-rsrources - unsetting the project
#
tanzu project unset 
tanzu context list  $w
k api-resources | wc -l
#

```

The output (Notice: The various api-resources (wc -l) 23-29-27-20-23)

```

[root@orfdns ~]# 
[root@orfdns ~]# export proj="AMER-East"
[root@orfdns ~]# export sp="orfspace1"
[root@orfdns ~]# export org="sa-tanzu-platform"
[root@orfdns ~]# export cl="orfclustergroup"
[root@orfdns ~]# export w=''
[root@orfdns ~]# #export w='--wide'
[root@orfdns ~]# #
[root@orfdns ~]# #Results in 23 api-resources - just loggin in
[root@orfdns ~]# #
[root@orfdns ~]# yes | tanzu context delete $org
Deleting the context entry from the config will remove it from the list of tracked contexts. You will need to use `tanzu context create` to re-create this context. Are you sure you want to continue? [y/N]: [i] Deleting kubeconfig context 'tanzu-cli-sa-tanzu-platform' from the file '/root/.config/tanzu/kube/config'
[!] WARNING: this removed your active context, use "kubectl config use-context" to select a different one
[ok] Successfully deleted context "sa-tanzu-platform"
[root@orfdns ~]# source ./tanzucli.src
[root@orfdns ~]# tanzu login
[i] API token env var is set

[ok] Successfully logged into 'sa-tanzu-platform' organization and created a tanzu context
[root@orfdns ~]# tanzu context list $w
  NAME               ISACTIVE  TYPE   PROJECT  SPACE  
  sa-tanzu-platform  true      tanzu                  

[i] Use '--wide' to view additional columns.
[root@orfdns ~]# k api-resources | wc -l
23
[root@orfdns ~]# #
[root@orfdns ~]# #Results in 29 api-resources - setting the Project
[root@orfdns ~]# #
[root@orfdns ~]# tanzu project use $proj
✓ Successfully set project to AMER-East
[root@orfdns ~]# tanzu context list  $w
  NAME               ISACTIVE  TYPE   PROJECT    SPACE  
  sa-tanzu-platform  true      tanzu  AMER-East         

[i] Use '--wide' to view additional columns.
[root@orfdns ~]# k api-resources | wc -l
29
[root@orfdns ~]# #
[root@orfdns ~]# #Results in 27 api-resources - setting the cluster group
[root@orfdns ~]# #
[root@orfdns ~]# tanzu operations clustergroup use  $cl
ℹ  project has been set to AMER-East
ℹ  successfully set clustergroup to orfclustergroup
[root@orfdns ~]# tanzu context list  $w
  NAME               ISACTIVE  TYPE   PROJECT    SPACE  CLUSTERGROUP     
  sa-tanzu-platform  true      tanzu  AMER-East         orfclustergroup  

[i] Use '--wide' to view additional columns.
[root@orfdns ~]# k api-resources | wc -l
27
[root@orfdns ~]# #
[root@orfdns ~]# #
[root@orfdns ~]# #Results in 20 api-resources - setting the space
[root@orfdns ~]# #
[root@orfdns ~]# tanzu space use $sp 
✓ Successfully set space to orfspace1
[root@orfdns ~]# k api-resources | wc -l
20
[root@orfdns ~]# tanzu context list  $w
  NAME               ISACTIVE  TYPE   PROJECT    SPACE      
  sa-tanzu-platform  true      tanzu  AMER-East  orfspace1  

[i] Use '--wide' to view additional columns.
[root@orfdns ~]# #
[root@orfdns ~]# #Results in 23 api-rsrources - unsetting the project
[root@orfdns ~]# #
[root@orfdns ~]# tanzu project unset 
✓ Successfully unset the project, using org sa-tanzu-platform
[root@orfdns ~]# tanzu context list  $w
  NAME               ISACTIVE  TYPE   PROJECT  SPACE  
  sa-tanzu-platform  true      tanzu                  

[i] Use '--wide' to view additional columns.
[root@orfdns ~]# k api-resources | wc -l
23
[root@orfdns ~]#

```
# Space enablement turns yellow

In my case the cause was that the capabilities in the space and in the cluster group did not match (Kirti's example in picture). 

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/kirtiyellowspace.png)

Cluster Capabilities vs. Space Capabilities matchup (things are not in alinment) 

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/kirticapabilitiesclustergroupandspace.png)

Automate way to analyse the space vs. cluster group differences

```
source tanzucli.src
export proj="AMER-East"
export sp="orfspace1"
export org="sa-tanzu-platform"
export cl="orfclustergroup"
export w=''
#export w='--wide'
export line="-----------------------------------------------------------------"
yes | tanzu context delete $org
source ./tanzucli.src
tanzu login
tanzu project use $proj
tanzu operations clustergroup use  $cl
echo $line > /tmp/clustergroup.txt
echo "Cluster Group Capabilities" >>  /tmp/clustergroup.txt
echo $line >> /tmp/clustergroup.txt
k get kubernetescluster orfscluster -o yaml | grep -A 1000 capabilities: | grep name: | awk '{ print $2 }' | sort >> /tmp/clustergroup.txt
tanzu space use $sp 
echo $line > /tmp/space.txt
echo "Space Capabilities" >>  /tmp/space.txt
echo $line >> /tmp/space.txt
tanzu space get orfspace1 | grep  -e '^   -' | awk '{ print $2 }' | sort >> /tmp/space.txt
sdiff /tmp/clustergroup.txt /tmp/space.txt
#
```

Outcome: In my case the clustergroup has more but more importanlly the space capablities exist in the cluster group. 

```
sdiff /tmp/clustergroup.txt /tmp/space.txt
-------------------------------------------------------------   -------------------------------------------------------------
Cluster Group Capabilities                                    | Space Capabilities
-------------------------------------------------------------   -------------------------------------------------------------
bitnami.services.tanzu.vmware.com                             <
certificates.tanzu.vmware.com                                   certificates.tanzu.vmware.com
config-server.spring.tanzu.vmware.com                         <
container-app.tanzu.vmware.com                                  container-app.tanzu.vmware.com
crossplane.tanzu.vmware.com                                   <
egress.tanzu.vmware.com                                       <
fluxcd-helm.tanzu.vmware.com                                  <
fluxcd-source.tanzu.vmware.com                                <
k8sgateway.tanzu.vmware.com                                   <
mtls.tanzu.vmware.com                                         <
multicloud-ingress.tanzu.vmware.com                           <
observability.tanzu.vmware.com                                <
package-management.tanzu.vmware.com                           <
registry-pull-only-credentials-installer.tanzu.vmware.com     <
servicebinding.tanzu.vmware.com                               <
servicemesh-observability.tanzu.vmware.com                    <
[root@orfdns ~]# 
```

