# Bold BI on Microsoft Azure Kubernetes Service

For fresh installation, continue with the following steps to deploy Bold BI On-Premise in Microsoft Azure Kubernetes Service (AKS).

* Create a Kubernetes cluster in Microsoft Azure Kubernetes Service (AKS) to deploy Bold BI.

* Create a File share instance in your storage account and note the File share name to store the shared folders for applications’ usage.

* Encode the storage account name and storage key in base64 format.

* Connect with your Microsoft AKS cluster.

* After connecting with your cluster, deploy the latest Nginx ingress controller to your cluster using the following command.

```sh
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.41.2/deploy/static/provider/cloud/deploy.yaml
```

* Run the following command to install Bold BI.

```sh
helm install <Release Name> boldbi-helmchart --set appBaseUrl=<Host URL>,persistentVolume.aks.fileShareName=<File share name>,persistentVolume.aks.azureStorageAccountName=<base64_azurestorageaccountname>,persistentVolume.aks.azureStorageAccountKey=<base64_azurestorageaccountkey>
```

* Read the optional client library license agreement from the following link.

    [Consent to deploy client libraries](../docs/consent-to-deploy-client-libraries.md)

* Note the optional client libraries from the above link as comma separated names and replace it in `<comma_separated_library_names>` place.

```sh
helm install <Release Name> boldbi-helmchart --set appBaseUrl=<Host URL>,persistentVolume.aks.fileShareName=<File share name>,persistentVolume.aks.azureStorageAccountName=<base64_azurestorageaccountname>,persistentVolume.aks.azureStorageAccountKey=<base64_azurestorageaccountkey>,optionalLibs=<comma_separated_library_names>
```

* If you need to use **Bing Map** widget feature, enter value for `widget_bing_map_enable` environment variable as `true` and API key value for `widget_bing_map_api_key` on **deployment.yaml** file.
   
```sh
helm install <Release Name> boldbi-helmchart --set appBaseUrl=<Host URL>,persistentVolume.aks.fileShareName=<File share name>,persistentVolume.aks.azureStorageAccountName=<base64_azurestorageaccountname>,persistentVolume.aks.azureStorageAccountKey=<base64_azurestorageaccountkey>,bingMapWidget.enabled=true,bingMapWidget.apiKey=<api-key>
``` 

* Wait for some time till the Bold BI On-Premise application deployed to your Microsoft AKS cluster.

* Use the following command to get the pods’ status.

```sh
kubectl get pods -n boldbi
```
![Pod status](images/pod_status.png) 

* Configure the Bold BI On-Premise application startup to use the application. Please refer the following link for more details on configuring the application startup.
    
    https://help.boldbi.com/embedded-bi/application-startup
