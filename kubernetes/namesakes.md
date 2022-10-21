# *Working with Kubernetes Namesakes*

situation-

You are working for BeeBox, a subscription service company that provides weekly shipments of bees to customers.
The company is in the process of containerizing their infrastructure and running their software on Kubernetes. 
As part of this process, the company is working on determining what namespaces it will need in the Kubernetes cluster.

You have been asked to access the cluster and perform some maintenance tasks related to the cluster's namespaces.

The dev team would like a namespace they can work in that is separate from namespaces used to run production workloads. 
Create a new namespace called dev.
One of the members of your security team would like to audit the namespaces that currently exist in the cluster. 
Get a list of the current namespaces and save it to a file located at /home/cloud_user/namespaces.txt on the control plane node.
Someone on the team created a pod with the name quark, but they are not sure which namespace it is in. 
Determine which namespace this pod is in, and save the name of that namespace to a file located at /home/cloud_user/quark-namespace.txt on the control plane node.

<img width="556" alt="name_onw" src="https://user-images.githubusercontent.com/94250541/197278015-ed0c4112-1ac2-46a3-bef8-ffe911cccebb.png">

<img width="560" alt="name_two" src="https://user-images.githubusercontent.com/94250541/197278034-ebaa5b76-9948-4770-85d9-babd9995d542.png">

<img width="553" alt="name_three" src="https://user-images.githubusercontent.com/94250541/197278045-bc1f2024-f8eb-4cda-9424-f150dcda8631.png">
