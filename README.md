# turbine-server
___

## Turbine server for TIBCO BWCE 
### Environment Variables -

PLATFORM = Openshit/Kubernetes (Default - Kubernetes)

NAMESPACE = k8s namespace to monitor (Default - Current Namespace)

### Label Selector

By default, no applications are polled for hystrix stream.  
To include a particular application, add the following label to deployments. 

hystrix.enabled=true

### Build docker image

From the project path, execute -

mvn clean package docker:build

### Monitoring applications in projects/namespaces other than current

Permissions need to be provided to view services from other projects/namespaces.

##### Kubernetes (Tested on minikube) 
Add clusterrolebinding
  
kubectl create clusterrolebinding [hystrix-namespace] --clusterrole cluster-admin --serviceaccount=[hystrix-namespace]:[user]

##### Openshift 
oc project [project to monitor]
  
oc policy add-role-to-user view system:serviceaccount:[hystrix-namespace]:[user]
