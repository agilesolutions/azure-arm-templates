# Starter project on ARM templates


## Parameters
* aksClusterName: Name of the AKS cluster.
* dnsPrefix: DNS prefix for the cluster.
* agentCount: Number of Linux nodes (default is 1).
* agentVMSize: Specifies the VM size for the nodes.
* kubernetesVersion: The version of Kubernetes to use.
* location: Location of the cluster.

## Resources
* Creates an AKS cluster with one Linux node in the System mode agent pool.

## Outputs
* aksClusterName: Outputs the name of the AKS cluster.
* resourceGroupName: Outputs the name of the resource group.
* kubeConfigCommand: Provides the command to retrieve kubeconfig to manage the cluster.

## Deployment
```
az deployment group create \
  --resource-group <resource-group-name> \
  --template-file <path-to-template.json> \
  --parameters aksClusterName=<your-cluster-name> dnsPrefix=<your-dns-prefix>

```

## Instructions
* Save ARM template as azuredeploy.json and create corresponding azuredeploay.parameters.json with required parameters.
* add YAML pipeline to Azure DevOps repository.
* Replace YourAzureServiceConnection with the name of your Azure service connection in Azure DevOps
* Run the pipeline to deploy the cluster.

## Command to Validate ARM Templates
```
az deployment group validate \
  --resource-group <resource-group-name> \
  --template-file <template-file-path> \
  --parameters <parameters-file-path>

```
* resource-group-name : The name of the Azure resource group where you intend to deploy the template.
* template-file-path : The path to your ARM template JSON file (e.g., azuredeploy.json).
* parameters-file-path : The path to the parameters file (e.g., azuredeploy.parameters.json).

## Example
```
az deployment group validate \
  --resource-group myResourceGroup \
  --template-file azuredeploy.json \
  --parameters azuredeploy.parameters.json
```

## Expected output
```
{
  "properties": {
    "provisioningState": "Succeeded",
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "timestamp": "2025-01-21T12:34:56.7890123Z",
    "outputs": null
  }
}
```

## Additional Validation options
```
az deployment sub validate \
  --location <location> \
  --template-file <template-file-path> \
  --parameters <parameters-file-path>

```

