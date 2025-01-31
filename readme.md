This is a quick workshop format demonstration of Red Hat Virtualization on ROSA.
Red Hat OpenShift Virtualization is based on the Kubevirt OpenSource project delivered via ROSA. 
ROSA is the joint AWS and Red Hat managed service based on OpenShift delivered as a console service in AWS. 
Virtualization on ROSA gives you the ability to host Virtual Machines of Linux and Windows with Containers on ROSA. 
By Andrew Grimes with videos from Alan Cowles, Jim Garrett and Mayur Shetty 
Verified Working  01/26/25
No Longer Maintained 


Basic ROSA Overview Video https://www.youtube.com/watch?v=6W-xDavWgYg&t=4s



Joint AWS and Red Hat Blog on Virtualization on ROSA for the value prop
https://www.redhat.com/en/blog/managing-virtual-machines-and-containers-as-code-with-openshift-virtualization-on-red-hat-openshift-service-on-aws


This Workshop assumes you are using a ROSA instance created out of the Red Hat Demonstration System (RHPDS) for a Demo or POC. We use EBS local storage so live migration is not supported with EBS Storage. We support other storage services and will support more partner services in the future if live migration, hybrid use cases or data protection integraiton is required. These procedures are optimized for RHPDS demo system but the procedures should work in any account context if needed. Please note we require "bare metal" workers for ROSA to work and those are more expensive than regular EC2 Instances so we suggest setting cost alerts on your account and shutting down the workshop when not in use. 

Virtualization on ROSA Catalog. 
<p align="left">
  <a href="#"><img src="./console.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

Below are te instructions and Links for a quick Virtualization on ROSA Install and Setup for a Basic Demo of the serve. 
This uses local EBS storage so live migration is not available. We recommend deleting your lab when not in use as the VM’s can be expensive. 
The AWS FSXN service with NFS as well as Pure Portworx are also supported options. ODF is planned for a future release for storage. 

The below steps "assumes" you have RHPDs access to the ROSA Open Lab setup to execute the following steps again. This will create a Container Image Classifications Container App with Fedora, RHEL and Windows Virtual machines created from ISO images.  

#1 Use this link to create a Basic ROSA Cluster via RHPDS or installed in single AZ (2 workers) 
https://demo.redhat.com/catalog?item=babylon-catalog-prod/sandboxes-gpte.rosa.prod&utm_source=webapp&utm_medium=share-link


Lab Used for this workshop in RHPDS, avaialble to AWS and Partners, check with your account team for a Level Up Demo. 
<p align="left">
  <a href="#"><img src="./labtile.jpg" width="200"></a> <br />
  <em> 
  </em>
</p>

#2 Using your Red Hat ID, collect your console token for your Red Hat ID, and Install with your personal Token so you can use the Hybrid Cloud Console Later to "add" workers to your cluster via the Red Hat system. https://console.redhat.com/openshift/token/rosa

#3 Verify cluster install is complete by logging onto the ROSA console and checking status. CLI is not required but we do recommend using VS Code with the OpenShift plugin to update configuration files. 

#4 Login to the ROSA console and then use the Cluster Manager link to get to “your” hybrid cloud console via token access. If you didn't use a token, your access won't work. The Red Hat Hybrid Cloud Console supports maintenance activity and allows you to "add" workers to your cluster. (use the link off your ROSA console is the preferred way to get your cluster but here is the direct link. 
https://console.redhat.com/openshift/

Your ROSA console will have this link on the home page to directly link to the cluster manager where you can add your machine pool for bare metal workers.  
<p align="left">
  <a href="#"><img src="./console_hybrid.jpg" width="200"></a> <br />
  <em> 
  </em>
</p>

#5 Use the hybrid cloud console to get to your cluster directly and click machine pool and then add, select metal worker and add 2 with auto scaling setup to 3 M5.metal is the ideal case. 

M5zn.metal is a cheaper option (48vCPU vs 96 vCPU) and half the cost on AWS side
The full list is here https://aws.amazon.com/marketplace/pp/prodview-tnyp2h3acabm6

Using the Hybrid Cloud Console use add machine pool to add a supported Bare Metal Worker. 
<p align="left">
  <a href="#"><img src="./machinepool_add.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>


#6 Check your Console for worker building status it will show “creating” 0/2 until complete. Takes about 45 min. 
This is visible under the Admin Main conosole in Compute, Machine Set. 

On the ROSA Console use Compute, Machine Set to check on worker add status. This will take approx 30-45min. 
<p align="left">
  <a href="#"><img src="./worker_add_status.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>


#7 In parallel to the bare metal machine pool, Install OpenShift Virtualization in the Operator Hub, install “OpenShift Virtualization" and take defaults. Install to all accounts. 

OpenShift Virtualization Operator Install process is on the ROSA Console.  
<p align="left">
  <a href="#"><img src="./ROSA_Operator.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

#8 Create a Hyperconverged instance as well with defaults in the CNV namespace. Once complete this will trigger a reload of the console to make the "Virtualization" menu visible. 

Add HyperConverged Space to the Operator to deploy VM's. 
<p align="left">
  <a href="#"><img src="./hyperconverged_add2.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

#9 Create a linuxvm project under developer profile to deploy your applications into so they are isolated from other workloads but they can be grouped to "share" the application namespace. 

#10 Optional: add Container workload to a project if you want a mixed environment demo to show the VM's and containers interacting. 
Deploy backend: https://github.com/emcon33/inference-rosa-workshop
Deploy frontend:  https://github.com/emcon33/inference-rosa-frontend

#10 When OpenShift Virtualization Operator is installed, the console will request an update: Refresh to see virt tools show up in the side menu. Verify they are visible and avaialable. 

This banner will appear once the Operator and Hyperconverged space is installed. 
<p align="left">
  <a href="#"><img src="./update.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>


#11 Verify your Workers are completed import and installed under Compute, Machine Set, once it is 2/2 you can create a VM once they are added and online. 

#12 Create a RHEL or Fedora VM using “defaults” in the linuxvm project, save the password from the optional tab to login later. 
By defaul the RHEL, Fedora and CentOS ISO's are included for installation. Windows requires you upload an ISO or use a URL to link to the ISO. 
The default user name for RHEL and Fedora are  
Fedora Default User: "fedora" & RHEL Default User: "cloud_user"

Console Catalog of Virtualization Services. 
<p align="left">
  <a href="#"><img src="./console.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

Default Fedora Creation Panel.  
<p align="left">
  <a href="#"><img src="./fedora_create.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

Fedora Optional Install panel with install password. 
<p align="left">
  <a href="#"><img src="./fedora_optional.jpg" width="600"></a> <br />
  <em> 
  </em>


#13 VM “provisioning” will take about 10min and your up, access via the console tab and use the logon and password from above. 


#14 You are now up and running with a VM, add it to the app space with containers to show a mixed environment. Extract your YAML and use that in a pipeline/gitops etc. 

Fedora Install look with console. 
<p align="left">
  <a href="#"><img src="./fedora_install.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

#15 You can associate the VM with your application grouping and you now have a hybrid application of containers and VM's 

Hybrid App of VM's and Containers. 
<p align="left">
  <a href="#"><img src="./hybrid_app_rosa.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

#16 For a Windows image, you need to upload an ISO or obtain an iso URL and install from image using defaults. 
Obtain Windows 10 ISO here https://www.microsoft.com/en-us/software-download/windows10ISO
Obtain Windows 11 ISO here https://www.microsoft.com/software-download/windows11

Download, or select the options until you start the download and use that URL if you want a direct to ROSA
We are not providing a Windows lic. 

Steps to build windows:  

Select Create VVM from Template/catalog and select Windows 10 and options

Select boot from CD

Put in the URL you obtained below from the Windows ISO website 
this is a 5GB file so upload will take some time, the URL method took about 5min

Windows 10 Setup will look like this on ROSA Classic 4.14.x 
<p align="left">
  <a href="#"><img src="./windows10_install.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

Windows 10 Setup will look like this on ROSA HCP 4.15.14 
<p align="left">
  <a href="#"><img src="./Windows_create_iso.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>


Windows on ROSA deployed with console access. 
<p align="left">
  <a href="#"><img src="./windows_rosa.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

You now have a Windows Live Image, you can step through the install steps. If you performed the prior setup you now have a Hybrid App with Containeres, RHEL, Fedora and Windows 10 images all available. 

Hybrid App with Linux, Windows and Containers integrated. 
<p align="left">
  <a href="#"><img src="./hybrid_app_rosa2.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

Here is a Direct Link to Windows 10 64bit English ISO: 
https://software.download.prss.microsoft.com/dbazure/Win10_22H2_English_x64v1.iso?t=1182d063-b4cc-4e05-b23b-b0e360f24bef&P1=1711927623&P2=601&P3=2&P4=STgkkfcF8I2W9rpuFC0kO9LrUryOUY8rzB7LPCAya1YuUA56eKW205X624OD6uE%2fkSniKcF5esmiKlzkcEOCPaEz%2b4pEIq%2fONKP%2fzXS7%2bn7e8g%2bXgQmDsecmzWf29%2b%2b0aJNd2fDey2IOxG8o1LrKczfp8P5YlhiODB20CsoUuzkuMzVJNHcy3J7UDzR%2bmSaAM2wacQ11%2f4bD89%2fAnSMsm8yj5xZv3PrvmBrg%2fkPE1LzvSeQbbkLgc5KaOkCilnrbY%2b07UwRl1L3nN%2fMay9fhACdquTOrnlDWNMGkzAuxF9t2Yo1XV7%2bt596dISKNOQZ4xO2CU%2bvXg9Ppht3uWkcuaw%3d%3d


#17 Treating your VM's as code buy using YAML to deploy images and create from YAML file. 
Sample Windows VM YAML (needs to be tested, may need to update the URL link to work) 

Windows YAML https://github.com/emcon33/Virtualization-on-ROSA/Windows10_create.yaml

Fedora YAML https://github.com/emcon33/Virtualization-on-ROSA/blob/fedora.yaml

Create a windows image by YAML file, you can use "create vm, YAML template and cut and paste the above into the window and then create. 
You an generate the YAML file by doing a grpahical create step and then save the YAML to a file. 
<p align="left">
  <a href="#"><img src="./windows_yaml_create.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>

#18 WIP Setup ArgoCD and use it to manage the YAML lifecycle of your VM and container deployments. 
ArgoCD Setup instructions 
Windows Images via ArgoCD 

Install and Setup ArgoCD on ROSA
ArgoCD Setup Blog: https://github.com/siamaksade/openshift-gitops-getting-started

ArgoCD Documentation: https://docs.openshift.com/container-platform/4.10/cicd/gitops/setting-up-argocd-instance.html

Install Operator
<p align="left">
  <a href="#"><img src="./argocd_operator.jpg" width="200"></a> <br />
  <em> 
  </em>
</p>

Your Instance will have a default ArgoCD on ROSA namespace under OpenShift Gitops, get your console link to login. 
Use "use Openshift" to login to your Argo CD Instance
<p align="left">
  <a href="#"><img src="./argocd_route.jpg" width="800"></a> <br />
  <em> 
  </em>
</p>

Setup ArgoCD App
<p align="left">
  <a href="#"><img src="./argocd_app_setup.jpg" width="800"></a> <br />
  <em> 
  </em>
</p>
https://argo-cd.readthedocs.io/en/stable/getting_started/

WIP: Create pipeline for VM creation

WIP: Create VM via ArgoCD
Windows VM Pipelines
https://github.com/kubevirt/kubevirt-tekton-tasks/tree/main/release/pipelines/windows-efi-installer

https://github.com/tosin2013/openshift-virt-tekton-ref
https://github.com/tosin2013/openshift-virt-tekton-ref/tree/main/docs

Manage a VM with ArgoCD on OpenShift Virtualization with ACM
https://www.youtube.com/watch?v=37Lqe0Vdkcc&t=890s

#19 WIP Import a VM into Virtualization on ROSA
(this requires a vSphere or VMC cluster image to import by MTV)

Virtualizaiton on ROSA vid 3 import VM https://www.youtube.com/watch?v=5zossjikJm8&t=1s

MTV Migration tool overview: https://www.youtube.com/watch?v=Fid24-qHHtU

#20 WIP: Ansible Automaing VM Management on OCP-Virt (applies to ROSA)

VM migration to OCP-Virt and Ansible https://www.youtube.com/watch?v=GZFhJerI9bo

Ansible VM management in OpenShift Virtualization on ROSA

<p align="left">
  <a href="#"><img src="./cloud_ansible_vm.jpg" width="600"></a> <br />
  <em> 
  </em>
</p>


Partner Solutions that work with ROSA, subject to partner support statements and documentation 
Virtual Machines create a highly persistent image inside a K8s cluster that typically works to abstract out unique elements from a container. This will often bring up the need for cross AZ replication and backup of images to avoid loss of a stateful OS Image with all associated application elements. Red Hat has several ecosystem partners that assist with data proteciton of VM's. Live Migration of VM's also works with storage partners though local EBS is supported. Here is a sample of the Ecosystem Partners that work with Virtualization on ROSA. 

#21 Eco Partner Data Protection: Trelio Data Protection

Backup VM https://www.youtube.com/watch?v=lhXuW2ERKiA

Restore VM https://www.youtube.com/watch?v=IGeDT0sNu-Q

#22 Eco Partner: Kasten Veeam Data Protection 
Protecting VM's on OCP-Virt: https://www.youtube.com/watch?v=WZBS9mU_kSg


#23 Eco Partner: Storage Option Pure Portworx Storage and Data Protection 
Pure Portworx and ROSA Doc. https://www.purestorage.com/content/dam/pdf/en/white-papers/wp-portworx-redhat-openshift-aws.pdf

Pure Portworx Setup for Storage with Live Migration: https://www.youtube.com/watch?v=V2kdVwKCId0

Pure Portworx Data Protection with Virtualization on ROSA: https://www.youtube.com/watch?v=YIEQCZxzoU4


#24 Eco Partner: AWS FSXN supoprt for NFS storage and migration

File Services with FSXN: https://www.redhat.com/en/blog/fully-managed-shared-file-storage-for-rosa

https://docs.netapp.com/us-en/netapp-solutions/rhhc/rhhc-solutions.html#scenario-3-data-protection-and-migration-from-the-on-premises-environment-to-aws-environment


Supporting Resources Videos: 
You can also follow these videos by Alan Cowles 
Virtualization on ROSA vid 1 Setup New https://www.youtube.com/watch?v=wBtY3tvjtIU
Virtualization on ROSA vid 2 Create VM  https://www.youtube.com/watch?v=7EpmmUIhQ7c&t=52s
Virtualizaiton on ROSA vid 3 import VM https://www.youtube.com/watch?v=5zossjikJm8&t=1s

More Links
Virtualization on ROSA Learning Path https://cloud.redhat.com/learn/how-manage-virtual-machines-using-red-hat-openshift-virtualization-red-hat-openshift-service

