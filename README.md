# How to POC Tanzu Platform / Tanzu App Engine / Tanzu HUB 

Tanzu Platfom is the combination of several Tanzu products into one (Hub). 
This includes the former Tanzu Service Mesh (TSM) and Tanzu Mission Control (TMC) and more...

This document will focus on how to get Tanzu Platform connected with an on-prem vCenter and 
how to get the "ole" nginx pod working (i.e. Random Customer Application). 

Assumption for this document is that vCenter is set up with Advanced Loadbalancer (AVI) or NSX-T (WCP enabled) 
A namespace has been created in vCenter (with everything in working order in the namespace). 

## Select the VMware Tanzu Platform Tile from the Cloud Console
```
Currently unable to find similar section for Tanzu Platform (Made the internal TP channel aware) :
 
  Port 443 TMC outbound connectivity

  https://docs.vmware.com/en/VMware-Tanzu-Mission-Control/services/tanzumc-concepts/GUID-147472ED-16BB-4AAA-9C35-A951C5ADA88A.html

  *.tmc.cloud.vmware.com
  console.cloud.vmware.com

  https://docs.vmware.com/en/VMware-Tanzu-Platform/index.html
```
##  What are the Steps?
```
(1) Create a Cluster Group
(2) Register a TKG Instance (vCenter Supervisor cluster) 
(3) Create a workload cluster 
(4) Install Cluster Group Capabilities
(5) Create a Profile
(6) Create an Availability Target
(7) Create a Space
(8) Create my first simple app (Follow link)
(9) Tips and Tricks
      api-resource study
      capabilities / space analysis
      Reg Creads
      Aliases

```

## Console Tile (https://console.cloud.vmware.com/) 
(In my case my user ID is in an organization that has access to the tile (see doc))

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

## (4) Install Cluster Group Capabilities

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

For Metrix to be in your cluster please add obersability to the profile

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/metrixprofile1.png)

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/metrixprofile2.png)


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
export KUBECONFIG="/root/.config/tanzu/kube/config"
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
export KUBECONFIG="/root/.config/tanzu/kube/config"
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
tanzu space get $sp  | grep -A 10 Profiles | grep -B 10 Availability | grep -v Availability | grep -v Profiles | sed  '/^$/d' | awk '{ print $1}' > /tmp/prof.txt
for f in `cat /tmp/prof.txt` 
do
echo $line
echo $f
echo $line
tanzu profile get $f | grep -A 100 Capabilities
done

```

Outcome: In my case the clustergroup has more but more importanlly the space capablities exist in the cluster group. 

```
[root@orfdns ~]# sdiff /tmp/clustergroup.txt /tmp/space.txt
-------------------------------------------------------------   -------------------------------------------------------------
Cluster Group Capabilities                                    | Space Capabilities
-------------------------------------------------------------   -------------------------------------------------------------
bitnami.services.tanzu.vmware.com                             <
certificates.tanzu.vmware.com                                   certificates.tanzu.vmware.com
config-server.spring.tanzu.vmware.com                         <
container-app.tanzu.vmware.com                                  container-app.tanzu.vmware.com
crossplane.tanzu.vmware.com                                   <
egress.tanzu.vmware.com                                         egress.tanzu.vmware.com
fluxcd-helm.tanzu.vmware.com                                  <
fluxcd-source.tanzu.vmware.com                                <
k8sgateway.tanzu.vmware.com                                     k8sgateway.tanzu.vmware.com
mtls.tanzu.vmware.com                                         <
multicloud-ingress.tanzu.vmware.com                             multicloud-ingress.tanzu.vmware.com
observability.tanzu.vmware.com                                <
package-management.tanzu.vmware.com                             package-management.tanzu.vmware.com
registry-pull-only-credentials-installer.tanzu.vmware.com     <
servicebinding.tanzu.vmware.com                               <
servicemesh-observability.tanzu.vmware.com                    <
[root@orfdns ~]# tanzu space get orfspace1  | grep -A 10 Profiles | grep -B 10 Availability | grep -v Availability | grep -v Profiles | sed  '/^$/d' | awk '{ print $1}' > /tmp/prof.txt
[root@orfdns ~]# for f in `cat /tmp/prof.txt` 
> do
> echo $line
> echo $f
> echo $line
> tanzu profile get $f | grep -A 100 Capabilities
> done
-----------------------------------------------------------------
orfprofile1
-----------------------------------------------------------------
Required Capabilities
   - certificates.tanzu.vmware.com
   - container-app.tanzu.vmware.com
   - k8sgateway.tanzu.vmware.com
   - package-management.tanzu.vmware.com

Traits
   carvel-package-installer.tanzu.vmware.com - Resolved
    └─ carvel-package-installer
       └─ serviceAccountName: carvel-package-installer (editable)


-----------------------------------------------------------------
orf-custom-networking
-----------------------------------------------------------------
Required Capabilities
   - certificates.tanzu.vmware.com
   - egress.tanzu.vmware.com
   - multicloud-ingress.tanzu.vmware.com

Traits
   egress.tanzu.vmware.com - Resolved
    └─ egress.tanzu.vmware.com
       └─ open: false (editable)

   multicloud-cert-manager.tanzu.vmware.com - Resolved
    └─ multicloud-cert-manager.tanzu.vmware.com
       ├─ duration: 87600h (editable)
       ├─ name: default-issuer (editable)
       ├─ privateKey
       │  ├─ algorithm: ECDSA (editable)
       │  └─ size: 384 (editable)
       ├─ renewBefore: 2160h (editable)
       └─ selfSigned
          ├─ commonName: ca.company.biz (editable)
          └─ secretName: root-secret (editable)

   multicloud-ingress.tanzu.vmware.com - Resolved
    └─ multicloud-ingress.tanzu.vmware.com
       ├─ domain: tanzu.gelbrich.com (editable)
       ├─ gslb
       │  ├─ authentication
       │  │  └─ credentialRef: 02a169d1ffc75ae6b5bd55b2f7083e46 (editable)
       │  └─ dns
       │     └─ zoneId: Z05743862R5IXV6RNKGKE (editable)
       ├─ listenerTemplates: [map[namePrefix:https- port:443 protocol:HTTPS tls:map[secretRef:prod-certs]] map[namePrefix:http- port:80 protocol:HTTP]] (editable)
       ├─ name: default-gateway (editable)
       └─ useClusterIssuer: false (editable)

```

# Register Credentials

They are handled in the cluster capabilities

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/regcreds1.png)

![Version](https://github.com/ogelbric/POC_Tanzu_App_Engine/blob/main/regcreds2.png)

# Good to have aliases

```
alias l1='kubectl vsphere login --server 192.168.5.90 --vsphere-username administrator@vsphere.local --tanzu-kubernetes-cluster-namespace namespace1000 --tanzu-kubernetes-cluster-name orfscluster1 --insecure-skip-tls-verify'
alias l2='kubectl vsphere login --server 192.168.5.90 --vsphere-username administrator@vsphere.local --tanzu-kubernetes-cluster-namespace namespace1000 --tanzu-kubernetes-cluster-name orfscluster2 --insecure-skip-tls-verify'
alias l3='kubectl vsphere login --server 192.168.5.90 --vsphere-username administrator@vsphere.local --tanzu-kubernetes-cluster-namespace namespace1000 --tanzu-kubernetes-cluster-name orfscluster3 --insecure-skip-tls-verify'
alias tk='kubectl --kubeconfig ~/.config/tanzu/kube/config'
alias k='kubectl --kubeconfig ~/.kube/config'
alias t='tanzu'
```


Other Tools: 

```
https://github.com/mfine30/tanzu-tools
https://github.com/ogelbric/POC_Tanzu_App_Engine_Space_Trouble_Sooting_v1

```

# Tanzu CLI plugin update / check script

```
[root@orfdns ~]# ./tanzupluginanalysis.sh
----------------------------------------------------------------------------------------
accelerator kubernetes v1.10.0           upgradable to --> accelerator kubernetes v1.11.0
apply operations v0.1.7                  same version ---> apply operations v0.1.7
apps kubernetes v0.13.0                  same version ---> apps kubernetes v0.13.0
appsv2 global v0.2.2                     upgradable to --> appsv2 global v0.3.0
build global v0.9.2                      same version ---> build global v0.9.2
build-service kubernetes v1.0.0          same version ---> build-service kubernetes v1.0.0
clustergroup operations v0.1.10          same version ---> clustergroup operations v0.1.10
cluster operations v0.2.6                upgradable to --> cluster operations v0.2.7
context mission-control v0.1.15          same version ---> context mission-control v0.1.15
ekscluster operations v0.1.4             same version ---> ekscluster operations v0.1.4
external-secrets kubernetes v0.1.0       same version ---> external-secrets kubernetes v0.1.0
iam operations v0.1.9                    same version ---> iam operations v0.1.9
imgpkg global v0.3.5                     same version ---> imgpkg global v0.3.5
insight kubernetes v1.10.0               same version ---> insight kubernetes v1.10.0
isolated-cluster global v0.32.2          upgradable to --> isolated-cluster global v0.33.1
management-cluster kubernetes v0.32.2    upgradable to --> management-cluster kubernetes v0.33.1
management-cluster operations v0.1.4     same version ---> management-cluster operations v0.1.4
package kubernetes v0.35.0               same version ---> package kubernetes v0.35.0
pinniped-auth global v0.32.2             upgradable to --> pinniped-auth global v3.1.0
policy operations v0.1.12                same version ---> policy operations v0.1.12
project global v0.2.0                    upgradable to --> project global v0.2.2
provider-eks-cluster operations v0.1.4   same version ---> provider-eks-cluster operations v0.1.4
rbac global v0.1.1                       upgradable to --> rbac global v0.1.2
resource global v0.1.0                   upgradable to --> resource global v0.2.1
secret kubernetes v0.33.1                same version ---> secret kubernetes v0.33.1
services kubernetes v0.10.0              upgradable to --> services kubernetes v0.11.1
space global v0.2.0                      upgradable to --> space global v0.2.2
telemetry global v1.1.0                  same version ---> telemetry global v1.1.0
telemetry kubernetes v0.33.1             same version ---> telemetry kubernetes v0.33.1
----------------------------------------------------------------------------------------
[root@orfdns ~]# ./tanzupluginanalysis.sh --upgrade --test
----------------------------------------------------------------------------------------
accelerator kubernetes v1.10.0           upgradable to --> accelerator kubernetes v1.11.0
tanzu plugin upgrade accelerator --target kubernetes
apply operations v0.1.7                  same version ---> apply operations v0.1.7
apps kubernetes v0.13.0                  same version ---> apps kubernetes v0.13.0
appsv2 global v0.2.2                     upgradable to --> appsv2 global v0.3.0
tanzu plugin upgrade appsv2 --target global
build global v0.9.2                      same version ---> build global v0.9.2
build-service kubernetes v1.0.0          same version ---> build-service kubernetes v1.0.0
clustergroup operations v0.1.10          same version ---> clustergroup operations v0.1.10
cluster operations v0.2.6                upgradable to --> cluster operations v0.2.7
tanzu plugin upgrade cluster --target operations
context mission-control v0.1.15          same version ---> context mission-control v0.1.15
ekscluster operations v0.1.4             same version ---> ekscluster operations v0.1.4
external-secrets kubernetes v0.1.0       same version ---> external-secrets kubernetes v0.1.0
iam operations v0.1.9                    same version ---> iam operations v0.1.9
imgpkg global v0.3.5                     same version ---> imgpkg global v0.3.5
insight kubernetes v1.10.0               same version ---> insight kubernetes v1.10.0
isolated-cluster global v0.32.2          upgradable to --> isolated-cluster global v0.33.1
tanzu plugin upgrade isolated-cluster --target global
management-cluster kubernetes v0.32.2    upgradable to --> management-cluster kubernetes v0.33.1
tanzu plugin upgrade management-cluster --target kubernetes
management-cluster operations v0.1.4     same version ---> management-cluster operations v0.1.4
package kubernetes v0.35.0               same version ---> package kubernetes v0.35.0
pinniped-auth global v0.32.2             upgradable to --> pinniped-auth global v3.1.0
tanzu plugin upgrade pinniped-auth --target global
policy operations v0.1.12                same version ---> policy operations v0.1.12
project global v0.2.0                    upgradable to --> project global v0.2.2
tanzu plugin upgrade project --target global
provider-eks-cluster operations v0.1.4   same version ---> provider-eks-cluster operations v0.1.4
rbac global v0.1.1                       upgradable to --> rbac global v0.1.2
tanzu plugin upgrade rbac --target global
resource global v0.1.0                   upgradable to --> resource global v0.2.1
tanzu plugin upgrade resource --target global
secret kubernetes v0.33.1                same version ---> secret kubernetes v0.33.1
services kubernetes v0.10.0              upgradable to --> services kubernetes v0.11.1
tanzu plugin upgrade services --target kubernetes
space global v0.2.0                      upgradable to --> space global v0.2.2
tanzu plugin upgrade space --target global
telemetry global v1.1.0                  same version ---> telemetry global v1.1.0
telemetry kubernetes v0.33.1             same version ---> telemetry kubernetes v0.33.1
----------------------------------------------------------------------------------------
[root@orfdns ~]# ./tanzupluginanalysis.sh --upgrade --yes
----------------------------------------------------------------------------------------
accelerator kubernetes v1.10.0           upgradable to --> accelerator kubernetes v1.11.0
[i] Installed plugin 'accelerator:v1.11.0' with target 'kubernetes'
[ok] successfully upgraded plugin 'accelerator'
apply operations v0.1.7                  same version ---> apply operations v0.1.7
apps kubernetes v0.13.0                  same version ---> apps kubernetes v0.13.0
appsv2 global v0.2.2                     upgradable to --> appsv2 global v0.3.0
[i] Installed plugin 'appsv2:v0.3.0' with target 'global'
[ok] successfully upgraded plugin 'appsv2'
build global v0.9.2                      same version ---> build global v0.9.2
build-service kubernetes v1.0.0          same version ---> build-service kubernetes v1.0.0
clustergroup operations v0.1.10          same version ---> clustergroup operations v0.1.10
cluster operations v0.2.6                upgradable to --> cluster operations v0.2.7
[i] Installed plugin 'cluster:v0.2.7' with target 'operations'
[ok] successfully upgraded plugin 'cluster'
context mission-control v0.1.15          same version ---> context mission-control v0.1.15
ekscluster operations v0.1.4             same version ---> ekscluster operations v0.1.4
external-secrets kubernetes v0.1.0       same version ---> external-secrets kubernetes v0.1.0
iam operations v0.1.9                    same version ---> iam operations v0.1.9
imgpkg global v0.3.5                     same version ---> imgpkg global v0.3.5
insight kubernetes v1.10.0               same version ---> insight kubernetes v1.10.0
isolated-cluster global v0.32.2          upgradable to --> isolated-cluster global v0.33.1
[i] Installed plugin 'isolated-cluster:v0.33.1' with target 'global'
[ok] successfully upgraded plugin 'isolated-cluster'
management-cluster kubernetes v0.32.2    upgradable to --> management-cluster kubernetes v0.33.1
[i] Installed plugin 'management-cluster:v0.33.1' with target 'kubernetes'
[ok] successfully upgraded plugin 'management-cluster'
management-cluster operations v0.1.4     same version ---> management-cluster operations v0.1.4
package kubernetes v0.35.0               same version ---> package kubernetes v0.35.0
pinniped-auth global v0.32.2             upgradable to --> pinniped-auth global v3.1.0
[i] Installed plugin 'pinniped-auth:v3.1.0' with target 'global'
[ok] successfully upgraded plugin 'pinniped-auth'
policy operations v0.1.12                same version ---> policy operations v0.1.12
project global v0.2.0                    upgradable to --> project global v0.2.2
[x] Failed to install plugin 'project:v0.2.2' with target 'global'
[x] : could not write file: write /root/.local/share/tanzu-cli/project/v0.2.2_b6ef98ae2dcd91b74f4827ad72c69fec755d5841dde47602fd7346b1c2de5c73_global: no space left on device
provider-eks-cluster operations v0.1.4   same version ---> provider-eks-cluster operations v0.1.4
rbac global v0.1.1                       upgradable to --> rbac global v0.1.2
[x] Failed to install plugin 'rbac:v0.1.2' with target 'global'
[x] : could not write file: write /root/.local/share/tanzu-cli/rbac/v0.1.2_4cf8c0b51c5357e95b29266cc0b1ba3c4da69e8000a77a908c627453b1cc07ea_global: no space left on device
resource global v0.1.0                   upgradable to --> resource global v0.2.1
[x] Failed to install plugin 'resource:v0.2.1' with target 'global'
[x] : could not write file: write /root/.local/share/tanzu-cli/resource/v0.2.1_66d905f3f70441f9331712d1fb07f0f7f0b581a9398638ba8a8a744d114b05c4_global: no space left on device
secret kubernetes v0.33.1                same version ---> secret kubernetes v0.33.1
services kubernetes v0.10.0              upgradable to --> services kubernetes v0.11.1
[x] Failed to install plugin 'services:v0.11.1' with target 'kubernetes'
[x] : could not write file: write /root/.local/share/tanzu-cli/services/v0.11.1_6143f5f61967d15e3fd81005b42a2abacf28bea978f5f8956a5ae3501f4f8afe_kubernetes: no space left on device
space global v0.2.0                      upgradable to --> space global v0.2.2
[x] Failed to install plugin 'space:v0.2.2' with target 'global'
[x] : could not write file: write /root/.local/share/tanzu-cli/space/v0.2.2_1da610ebf7b1404963dd129c3da27632e530d0d1ce581ebc6793c5aef634d49d_global: no space left on device
telemetry global v1.1.0                  same version ---> telemetry global v1.1.0
telemetry kubernetes v0.33.1             same version ---> telemetry kubernetes v0.33.1
----------------------------------------------------------------------------------------
[root@orfdns ~]# ./tanzupluginanalysis.sh
----------------------------------------------------------------------------------------
accelerator kubernetes v1.11.0           same version ---> accelerator kubernetes v1.11.0
apply operations v0.1.7                  same version ---> apply operations v0.1.7
apps kubernetes v0.13.0                  same version ---> apps kubernetes v0.13.0
appsv2 global v0.3.0                     same version ---> appsv2 global v0.3.0
build global v0.9.2                      same version ---> build global v0.9.2
build-service kubernetes v1.0.0          same version ---> build-service kubernetes v1.0.0
clustergroup operations v0.1.10          same version ---> clustergroup operations v0.1.10
cluster operations v0.2.7                same version ---> cluster operations v0.2.7
context mission-control v0.1.15          same version ---> context mission-control v0.1.15
ekscluster operations v0.1.4             same version ---> ekscluster operations v0.1.4
external-secrets kubernetes v0.1.0       same version ---> external-secrets kubernetes v0.1.0
iam operations v0.1.9                    same version ---> iam operations v0.1.9
imgpkg global v0.3.5                     same version ---> imgpkg global v0.3.5
insight kubernetes v1.10.0               same version ---> insight kubernetes v1.10.0
isolated-cluster global v0.33.1          same version ---> isolated-cluster global v0.33.1
management-cluster kubernetes v0.33.1    same version ---> management-cluster kubernetes v0.33.1
management-cluster operations v0.1.4     same version ---> management-cluster operations v0.1.4
package kubernetes v0.35.0               same version ---> package kubernetes v0.35.0
pinniped-auth global v3.1.0              same version ---> pinniped-auth global v3.1.0
policy operations v0.1.12                same version ---> policy operations v0.1.12
project global v0.2.0                    upgradable to --> project global v0.2.2
provider-eks-cluster operations v0.1.4   same version ---> provider-eks-cluster operations v0.1.4
rbac global v0.1.1                       upgradable to --> rbac global v0.1.2
resource global v0.1.0                   upgradable to --> resource global v0.2.1
secret kubernetes v0.33.1                same version ---> secret kubernetes v0.33.1
services kubernetes v0.10.0              upgradable to --> services kubernetes v0.11.1
space global v0.2.0                      upgradable to --> space global v0.2.2
telemetry global v1.1.0                  same version ---> telemetry global v1.1.0
telemetry kubernetes v0.33.1             same version ---> telemetry kubernetes v0.33.1
----------------------------------------------------------------------------------------
[root@orfdns ~]#

```


