# Up and running with WeaveWorks on AKS
## Prerequsites
1. Running AKS cluster 
2. Full admin access to AKS cluster
3. AZ CLI installed
4. Kubectl installed
5. CLI

## Ensure you have access to your cluster

__Run the following command:__<p>`kubectl get nodes`

If the output shows your nodes then you are good.

## Enable clusterbinding
You need to grant premissions for the installation on the AKS cluster.

__Run the following command__: <p>
`kubectl create clusterrolebinding "cluster-admin$(whoami)" --clusterrole=cluster-admin --user=kaleta`

__To install Weave Scope on AKS you need to run:__

`kubectl apply -f "https://cloud.weave.works/k8s/scope.yaml?k8s-version=$(kubectl version | base64 | tr -d '\n')"`

Now, verify that you the pods are up and running:

`kubectl get pods --all-namespaces`

**Notice that you now have a new namespace called weave**

**NAMESPACE   |     NAME                              READY     STATUS    RESTARTS   AGE**
weave         |     weave-scope-agent-4wdkm           1/1      Running    0          1d
weave         |     weave-scope-agent-rt4wm           1/1      Running    0          1d
weave         |     weave-scope-app-7f5f76bf89-clf6h  1/1      Running   0           1d


