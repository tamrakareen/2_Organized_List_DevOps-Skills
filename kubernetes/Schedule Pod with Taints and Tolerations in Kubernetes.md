# *Schedule Pod with Taints and Tolerations in Kubernetes*

Situation:

In this project, I will be presented with a three-node cluster. One node is the master, and the other two are worker nodes. I will be responsible for splitting up the two worker nodes and making one of the worker nodes a production (prod) environment node and the other a development (dev) environment node. The purpose of identifying these two types (prod and dev) is to not accidentally deploy pods into the production environment. You will use taints and tolerations to achieve this, and then I will deploy two pods: One pod will be scheduled to the dev environment, and one pod will be scheduled to the prod environment. 

Objectives:
1. Taint one of the worker nodes to repel work.
2. Schedule a pod to the dev environment.
3. Allow a pod to be scheduled to the prod environment.
4. Verify each pod has been scheduled and verify the toleration.

