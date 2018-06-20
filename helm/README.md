Helm on GKE cluster — quick hands-on guide

This quick guide helps with some practicalities on getting helm running on Google Kubernetes Engine (GKE) cluster. This article assumes that the reader:
Has prior knowledge about helm, kubernetes and gke.
Has a local installation ofkubectl andhelm also a GKE cluster with atleast 3 nodes (including master node).
This was tested with the following versions:

Create service account for helm
First create a service account and attach cluster-admin role to it. This enables the tiler pod to communicate with the kubernetes api. There are reasons why you should do this[1]. This can be done with kubectl apply -f <file>

Elevate privileges for creating ClusterRoleBindings (if necessary)
Skip this section if the above command was successful. Sometimes, you will end up with forbidden errors in GKE. A simpler way to solve this is by executing the ClusterRoleBinding as privileged user.
Obtain your admin password with gcloud describe

Revert back if you happen to elevate privileges, you do not need it anymore.
Initialise helm
Now run helm init passing the service account.

Verify helm
To start with, there should be at least a deployment and a service with name tiller-deployin kube-systemnamespace.

Create a samplechart and install it with name helm-test . This is going to install a simple nginx pod. Set the service type as LoadBalancer .
