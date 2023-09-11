# Ezmeral Data Fabric Helm
There are some variables are mendatory to set to deploy this helm chart.

Adding [[this repo link](https://github.com/p-grad/rancher-charts.git)](https://github.com/p-grad/rancher-charts.git) as Rancher repo, you will have the EDF CSI icon in the Rancher application list.  

This chart can be used to deploy EDF CSI on any Kubernetes cluster (not only Rancher managed). Just use:
``  
git clone  https://github.com/p-grad/rancher-charts.git  

cd rancher-charts/charts/edf-csi/1.0  

``  
Modify the *values.yaml* file  
And run helm command:  
``
helm install edf-csi --namespace edf-csi --create-namespace .
``

## Global Settings  
1. **Cluster Name  (required) *clusterName***  
The name of runcher cluster - The name is used as prefix for volumes mounted on Data Fabric 
  
2. **Use Airgap (required) *airgap.enabled***  
true or false (default false)
  
3. **Image Registry *airgap.registry***  
Airgap registry URL. Example: erm-airgap.ez.local:5000/airgap-ecp56  
Required only if *airgap.enabled* set to true  

## Data Fabric settings  
1. **Ticket *edf.ticket***  
The Data Fabric ticket generated on the EDF cluster  
The command to generate ticket is:  
```
maprlogin generateticket -type servicewithimpersonation -user mapr -cluster <ClusterName> -duration <Days>:<Hours>:<Mins> -out <outfile>  
```
Example:
```
maprlogin generateticket -type servicewithimpersonation -user mapr -cluster edf7.cluster.com -duration 100000:0:0 -out /tmp/maprticket  
```
The content of the outout file must be copied to the *edf.ticket* variable.  
  
2. **EDF Cluster Name *edf.clusterName***  
The name of the Data Fabric cluster  
  
3. **EDF CLDB Hosts *edf.cldbHosts***  
List of the Data Fabric CLDB hosts with port numbers, **space separated**.  
Example:
```
edf7-1.ez.local:7222 edf7-2.ez.local:7222 edf7-3.ez.local:7222  
```
  
4. **EDF Rest Servers *edf.restServers***  
List of the EDF Rest Servers with ports, **space separated**.  
Example:
```
edf7-1.ez.local:8443 edf7-2.ez.local:8443 edf7-3.ez.local:8443  
```
  
5. **Password Authentication *edf.PasswordAuthentication***  
true o false (default false). Choosing user/password authentication method to Rest Server  
If "false" - ticket authentication will be used  
  
6. **EDF Admin *edf.admin***  
The name of the Data Fabric administrator account (default mapr)  
Required only if *edf.PasswordAuthentication* set to true  
  
7. **EDF Password *edf.password***  
The passowrd of the EDF admin
Required only if *edf.PasswordAuthentication* set to true  
