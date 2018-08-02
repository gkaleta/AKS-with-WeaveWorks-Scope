# Up and running with WeaveWorks on AKS
## Prerequsites ![GitHub Logo](https://cloud.githubusercontent.com/assets/5456665/13322882/e74f6626-dc00-11e5-921d-f6d024a01eaa.png "GitHub")

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

::My usename is kaleta in this case::

__To install Weave Scope on AKS you need to run:__

`kubectl apply -f "https://cloud.weave.works/k8s/scope.yaml?k8s-version=$(kubectl version | base64 | tr -d '\n')"`

Now, verify that you the pods are up and running:

`kubectl get pods --all-namespaces`

**Notice that you now have a new namespace called weave**<p>

***NAMESPACE        NAME                              READY     STATUS    RESTARTS   AGE**<p><p>
`weave              weave-scope-agent-4wdkm           1/1      Running    0          1d<p>
weave              weave-scope-agent-rt4wm           1/1      Running    0          1d<p>
weave              weave-scope-app-7f5f76bf89-clf6h  1/1      Running    0          1d`<p>

## Run Scope in your browser and test everything out

`kubectl port-forward -n weave "$(kubectl get -n weave pod --selector=weave-scope-component=app -o jsonpath='{.items..metadata.name}')"`

**You should now be able to browse your localhost**<p>
`http://localhost:4040`

Alternatively, you can also expose the service through the loadbalancer - which means the whole world can access it:

`kubectl expose pod --namespace weave weave-scope-app-7f5f76bf89-clf6h --type=LoadBalancer`

## Dashboard examples of AKS running:

AKS Process overview:

![AKS Process overview](/images/aks-processes.png "AKS Process overview")

<p>
<p>
<p>

AKS Pod overview:

![AKS Process overview](/images/aks-pods.png "AKS pod overview")
