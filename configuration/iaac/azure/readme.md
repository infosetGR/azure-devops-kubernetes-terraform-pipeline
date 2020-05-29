

## Azure Marketplace

- Terraform 1 (https://marketplace.visualstudio.com/items?itemName=ms-devlabs.custom-terraform-tasks)
- Terraform 2 (https://marketplace.visualstudio.com/items?itemName=charleszipp.azure-pipelines-tasks-terraform)
- Aws (https://marketplace.visualstudio.com/items?itemName=AmazonWebServices.aws-vsts-tools)

## Azure Kubernetes Cluster

Pre-requisites
- Service Account
- SSH Public Key


```
# Create Service Account To Create Azure K8S Cluster using Terraform
az login
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/<<azure_subscription_id>>"

# Create Public Key for SSH Access
ssh-keygen -m PEM -t rsa -b 4096 # PEM - Privacy Enhanced Mail - Certificate Format RSA- Encryption Algorithm

# Remove storage lease in case of problem
az storage blob lease break -b kubernetes-dev.tfstate -c storageacctfotiscontainer --account-name storageacctfotis --account-key N3CFpRXbSnMPiZdxQy5gGMjN3Qt4t4fIB5NWuC1bayl7h3Wi7HfFhGQO+w8sAF49z2a3N93r7piLh4N2zZjS4w==

# ls /Users/rangakaranam/.ssh/id_rsa.pub

# Get Cluster Credentials
az aks get-credentials --name <<MyManagedCluster>> --resource-group <<MyResourceGroup>>
```
# get service (context change and we can fectch k8s external ip)
kubectl get svc