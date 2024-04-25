GitOps: Provision Fedora VM using ArgoCD
-----------------------------------------------------------------
Prequists : 
-----------
1) ROSA Cluster is up and running.
2) Baremetal Node added to the Machine to ROSA Cluster for VM provisioning. 
3) Red Hat GitOps Operator installed.
4) Red Hat Virtualization Operator installed and default HyperConverged created

Download the source code from below Github location
----------------------------------------------------
git clone https://github.com/dharmesh-b/fedora-vm-argocd-sample.git

login to as cluster-admin using
-------------------------------
oc login -u cluster-admin -p <<your password>> <<https://xxxx>>

Provision Fedora VM using below command
----------------------------------------
oc apply -k fedora-vm-argocd-sample/argocd-app
