This is a quick workshop format demonstration of Red Hat Virtualization on ROSA
Red Hat OpenShift Virtualization is based on the Kubevirt OpenSource project delivered via HCP
ROSA is the managed service based on OpenShift delivered as a Managed Service in AWS
Virtualization on ROSA is the ability to host Virtual Machines inside of Containers on ROSA
ROSA Overview Video https://www.youtube.com/watch?v=6W-xDavWgYg&t=4s

Joint AWS and Red Hat Blog on Virtualization on ROSA
https://www.redhat.com/en/blog/managing-virtual-machines-and-containers-as-code-with-openshift-virtualization-on-red-hat-openshift-service-on-aws

This Workshop assumes you are using a ROSA instance created out of the Red Hat Demonstration System for a Demo or POC. 
Many of the procedures will work in any account context if needed. Please note we require "bare metal" workers for ROSA to work and those are more expensive than regular EC2 Instances so we suggest setting cost alerts on your account and shutting down the workshop when not in use. 

<p align="left">
  <a href="#"><img src="./console.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

Quick Virtualization on ROSA Install and Setup for a Basic Demo
This uses local EBS storage so live migration is disabled. Delete your lab when not in use as the VM’s can be expensive. 

#1 Use a Basic ROSA Cluster via RHPDS or installed in single AZ (2 workers) 
https://demo.redhat.com/catalog?item=babylon-catalog-prod/sandboxes-gpte.rosa.prod&utm_source=webapp&utm_medium=share-link


Lab Used for this workshop in RHPDS, avaialble to AWS and Partners, check with your account team for a Level Up Demo 
<p align="left">
  <a href="#"><img src="./labtile.jpg" width="100"></a> <br />
  <em> 
  </em>
</p>

#2 Install with your personal Token for your Red Hat ID or personal ID so you can use the Hybrid Cloud Console Later to "add" workers to your cluster via the Red Hat system. 

#3 Verify cluster install is complete 

#4 Login to the console and then use the link to get to “your” hybrid cloud console, then add to machine pool.


#5 Use the hybrid cloud console to get to your cluster directly and click machine pool and then add, select metal worker and add 2 with auto scaling setup to 3
M5.metal is the ideal case. 
M5zn.metal is a cheaper option (48vCPU vs 96 vCPU) and half the cost on AWS side
https://aws.amazon.com/marketplace/pp/prodview-tnyp2h3acabm6

<p align="left">
  <a href="#"><img src="./machinepool_add.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>


#6  Check your Console for worker building status it will show “creating”  0/2 until complete. Takes about 45 min. 
This is visible under the Admin Main conosole in Compute, Machine Set

<p align="left">
  <a href="#"><img src="./worker_add_status.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>


#7 In parallel,  In the Operator Hub, install “OpenShift Virtualization and take defaults”

<p align="left">
  <a href="#"><img src="./ROSA_Operator.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

#8 Create a Hyperconverged instance as well with defaults

<p align="left">
  <a href="#"><img src="./hyperconverged_add2.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

#9 Create a linuxvm project under developer profile 

#10 Optional: add Container workload to a project if you want a mixed environment demo
backend: https://github.com/emcon33/inference-rosa-workshop
frontend:  https://github.com/emcon33/inference-rosa-frontend

#10 When Operatoor is installed, the console will request an update: Refresh to see virt tools

<p align="left">
  <a href="#"><img src="./update.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>


#11 Verify your Workers are installed under Compute, Machine Set, once it is 2/2 you can create a VM. 

#12 Create a RHEL or Fedora VM as “defaults” in the linuxvm project, save the password to login later. 
By defaul the RHEL, Fedora and CentOS ISO's are included for installation. Windows requires you upload an ISO. 
Save your password to log into later, it is under optional: 
Fedora User: fedora
RHEL User: cloud_user

<p align="left">
  <a href="#"><img src="./console.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

<p align="left">
  <a href="#"><img src="./fedora_create.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

<p align="left">
  <a href="#"><img src="./fedora_optional.jpg" width="600"></a> <br />
  <em> 
  </em>

#13 VM “provisioning” will take about 10min and your up




#14 You are now up and running with a VM, add it to a project with containers to show a mixed environment. Extract your YAML and use that in a pipeline/gitops etc. 

<p align="left">
  <a href="#"><img src="./fedora_install.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

#15 Associate with your application and you now have a hybrid application of containers and VM's 

<p align="left">
  <a href="#"><img src="./hybrid_app_rosa.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

#16 to add Windows you need to upload an ISO or obtain an iso URL and install from image
Obtain Windows ISO here https://www.microsoft.com/en-us/software-download/windows10ISO
Download, or select the options until you start the download and use that URL

Select Create VVM from Template and select Windows 10
Select boot from CD
Put in the URL you obtained below from the Windows ISO website 
this is a 5GB file so upload will take some time, the URL method took about 5min

<p align="left">
  <a href="#"><img src="./windows10_install.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>


<p align="left">
  <a href="#"><img src="./windows10_rosa.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

You now have a Windows Image. I fyou performed the prior setup you now have a Hybrid App with Containeres, RHEL, Fedora and Windows 10 images all available. 

<p align="left">
  <a href="#"><img src="./hybrid_app_rosa2.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

Direct Link to Windows 10 ISO: https://software.download.prss.microsoft.com/dbazure/Win10_22H2_English_x64v1.iso?t=1182d063-b4cc-4e05-b23b-b0e360f24bef&P1=1711927623&P2=601&P3=2&P4=STgkkfcF8I2W9rpuFC0kO9LrUryOUY8rzB7LPCAya1YuUA56eKW205X624OD6uE%2fkSniKcF5esmiKlzkcEOCPaEz%2b4pEIq%2fONKP%2fzXS7%2bn7e8g%2bXgQmDsecmzWf29%2b%2b0aJNd2fDey2IOxG8o1LrKczfp8P5YlhiODB20CsoUuzkuMzVJNHcy3J7UDzR%2bmSaAM2wacQ11%2f4bD89%2fAnSMsm8yj5xZv3PrvmBrg%2fkPE1LzvSeQbbkLgc5KaOkCilnrbY%2b07UwRl1L3nN%2fMay9fhACdquTOrnlDWNMGkzAuxF9t2Yo1XV7%2bt596dISKNOQZ4xO2CU%2bvXg9Ppht3uWkcuaw%3d%3d


#17 WIP: Treating your VM's as code with ArgoCD/Tekton
Setup Github and deploy VM's and containers by YAML
Deploy Windows/Linux from YAML with ArgoCD
https://drive.google.com/file/d/1Em6ZtRtpHR4ed4XJkcq9aNgAxRrx_lrP/view?usp=sharing

Windows Images via ArgoCD 
https://github.com/OOsemka/gitops-demo/tree/main

Windows VM Pipelines
https://github.com/kubevirt/kubevirt-tekton-tasks/tree/main/release/pipelines/windows-efi-installer

https://github.com/tosin2013/openshift-virt-tekton-ref
https://github.com/tosin2013/openshift-virt-tekton-ref/tree/main/docs






You can also follow these videos by Alan Cowles 
Virt on ROSA vid 1 Setup New https://www.youtube.com/watch?v=wBtY3tvjtIU
Virt on ROSA vid 2 Create VM  https://www.youtube.com/watch?v=7EpmmUIhQ7c&t=52s
Virtualizaiton on ROSA vid 3 import VM https://www.youtube.com/watch?v=5zossjikJm8&t=1s

More Links
Virtualization on ROSA Learning Path https://cloud.redhat.com/learn/how-manage-virtual-machines-using-red-hat-openshift-virtualization-red-hat-openshift-service


Storage Partners required for OpenShift Virtualization Live Motion on ROSA (thanks Mayur Shetty)
ROSA with FSXN Storage Blog Jan 10, 2024 (external)
https://www.redhat.com/en/blog/fully-managed-shared-file-storage-for-rosa

Pure Portworx with ROSA Virtualization 
Light Boards to post: (thanks Mayur Shetty)
https://www.youtube.com/watch?v=V2kdVwKCId0
https://www.youtube.com/watch?v=YIEQCZxzoU4

