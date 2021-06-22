# Bold BI on On-Premise Kubernetes Cluster

For fresh installation, continue with the following steps to deploy Bold BI application in your On-Premise machine kubernetes cluster.

1. Deploy the latest Nginx ingress controller to your cluster using the following command.

```sh
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.41.2/deploy/static/provider/cloud/deploy.yaml
```

2. Create a folder in your machine to store the shared folders for applications’ usage.

    Ex: `D://app/shared`

	mention this location in install command as like below
	
	Ex: D://app/shared -> /run/desktop/mnt/host/d/app/shared
	
3. Run the following command to install Bold BI.

```sh
helm install <Release Name> boldbi-helmchart --set appBaseUrl=<Host URL>,persistentVolume.onpremise.hostPath=/run/desktop/mnt/host/<local_directory>
```

4. Read the optional client library license agreement from the following link.

    [Consent to deploy client libraries](../docs/consent-to-deploy-client-libraries.md)

5. Note the optional client libraries from the above link as comma separated names and replace it in `<comma_separated_library_names>` place.

```sh
helm install <Release Name> boldbi-helmchart --set appBaseUrl=<Host URL>,persistentVolume.onpremise.hostPath=/run/desktop/mnt/host/<local_directory>,optionalLibs=<comma_separated_library_names>
```

6. If you need to use **Bing Map** widget feature, enter value for `widget_bing_map_enable` environment variable as `true` and API key value for `widget_bing_map_api_key` on **deployment.yaml** file.
   
```sh
helm install <Release Name> boldbi-helmchart --set appBaseUrl=<Host URL>,persistentVolume.onpremise.hostPath=/run/desktop/mnt/host/<local_directory>,bingMapWidget.enabled=true,bingMapWidget.apiKey=<api-key>
```

7.	Wait for some time till the Bold BI On-Premise application deployed to your On-Premise Kubernetes cluster. 

8.	Use the following command to get the pods’ status.

```sh
kubectl get pods -n boldbi
```
![Pod status](images/pod_status.png) 

9. After deployment, wait for some time to Horizontal Pod Autoscaler (HPA) gets the metrics from the pods. Use the following command to get HPA status.

```sh
kubectl get hpa -n boldbi
```
If you get `<unknown>/80%` instead of actual CPU and memory usage of pods, then you do not have any metrics server running inside your cluster. Use the following command to deploy metrics server in your cluster to enable the autoscaling feature by HPA.
    
```sh
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.3.7/components.yaml
```

10.	Use your DNS hostname to access the application in the browser.

11.	Configure the Bold BI On-Premise application startup to use the application. Please refer the following link for more details on configuring the application startup.
    
    https://help.boldbi.com/embedded-bi/application-startup