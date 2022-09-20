# Carson

in the folder that has docker-compose.yaml

`sudo docker compose up -d`

`sudo docker compose down`

`az acr login --name <acrName>`

where `<acrName>` = `*` = `caredotcoach`

`az group create --name <yourResourceGroup> --location westus2`

`sudo docker tag mcr.microsoft.com/azuredocs/azure-vote-front:v1 <acrLoginServer>/azure-vote-front:v1`

where `<acrLoginServer>` = `*.azurecr.io`

`sudo docker push <acrLoginServer>/azure-vote-front:v1`

```
az aks create \
    --resource-group yourResourceGroup \
    --name yourAKSCluster \
    --node-count 2 \
    --generate-ssh-keys \
    --attach-acr <acrName>
```

```
az aks create \
    --resource-group faraResourceGroup \
    --name faraAKSCluster \
    --node-count 2 \
    --generate-ssh-keys \
    --attach-acr caredotcoach
```

you may need to remove the `--attach-acr <acrName>` portion if you dont have permission

```
az aks get-credentials --resource-group faraResourceGroup --name faraAKSCluster
```

`kubectl apply -f azure-vote-all-in-one-redis.yaml`

`kubectl get service azure-vote-front --watch`

```
carson@fara-vm2:/fara/azure-voting-app-redis$ kubectl get service azure-vote-front --watch
NAME               TYPE           CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE
azure-vote-front   LoadBalancer   10.0.212.157   20.252.80.191   80:30970/TCP   6m
```

copy `20.252.80.191` and paste into your browser. You should see the app running. 

To delete a specific deployment

```
carson@fara-vm2:/fara/ml_fara$ kubectl get deployments --all-namespaces
NAMESPACE     NAME                 READY   UP-TO-DATE   AVAILABLE   AGE
default       azure-vote-back      1/1     1            1           114m
default       azure-vote-front     1/1     1            1           114m
default       convo-rec            1/1     1            1           97m
default       convo-rec-v2         1/1     1            1           38m
default       convo-rec2           1/1     1            1           42m
kube-system   coredns              2/2     2            2           5h14m
kube-system   coredns-autoscaler   1/1     1            1           5h14m
kube-system   konnectivity-agent   2/2     2            2           5h14m
kube-system   metrics-server       2/2     2            2           5h14m
```

Where NAMESPACE is the namespace it's in, and DEPLOYMENT is the NAME of the deployment. If NAMESPACE is default, leave off the -n option altogether.

`kubectl delete deployment convo-rec2`

# From Azure

---
page_type: sample
languages:
  - python
products:
  - azure
  - azure-redis-cache
description: "This sample creates a multi-container application in an Azure Kubernetes Service (AKS) cluster."
---

# Azure Voting App

This sample creates a multi-container application in an Azure Kubernetes Service (AKS) cluster. The application interface has been built using Python / Flask. The data component is using Redis.

To walk through a quick deployment of this application, see the AKS [quick start](https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough?WT.mc_id=none-github-nepeters).

To walk through a complete experience where this code is packaged into container images, uploaded to Azure Container Registry, and then run in and AKS cluster, see the [AKS tutorials](https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-app?WT.mc_id=none-github-nepeters).

## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
