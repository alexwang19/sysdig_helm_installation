# Sysdig Installation Steps


## START HERE


Options Available

[Install with proxy](#Install with proxy)
Installation with Proxy and Custom Image Repo(Internal Registry)
Basic installation with PriorityClass
Installation with Proxy with PriorityClass
Installation with Proxy and Custom Image Repo(Internal Registry) with PriorityClass
Basic installation with EBF enabled
Installation with Proxy with EBF enabled
Installation with Proxy and Custom Image Repo(Internal Registry) with EBF enabled
Basic installation with maxImageSize and ephemeralStorage Increase
Installation with Proxy with maxImageSize and ephemeralStorage Increase
Installation with Proxy and Custom Image Repo(Internal Registry) with maxImageSize and ephemeralStorage Increase
Basic installation with maxImageSize and ephemeralStorage Increase and EBF enabled
Installation with Proxy with maxImageSize and ephemeralStorage Increase and EBF enabled
Installation with Proxy and Custom Image Repo(Internal Registry) with maxImageSize and ephemeralStorage Increase and EBF enabled
Basic installation with maxImageSize and ephemeralStorage Increase and EBF enabled and PriorityClass
Installation with Proxy with maxImageSize and ephemeralStorage Increase and EBF enabled and PriorityClass
Installation with Proxy and Custom Image Repo(Internal Registry) with maxImageSize and ephemeralStorage Increase and EBF enabled and PriorityClass


Do you need proxy enabled?


## Basic installation
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)> \
-f static-values.yaml \
sysdig/sysdig-deploy
```

## Installation with Proxy
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)>
--set global.proxy.httpProxy=<Http Proxy> \
--set global.proxy.httpsProxy=<Https Proxy> \
--set global.proxy.noProxy="<No Proxy, comma delimited list>" \
--set agent.sysdig.settings.http_proxy.proxy_port=<Proxy Port> \
--set agent.sysdig.settings.http_proxy.proxy_host=<Proxy Host> \
-f static-values.yaml \
sysdig/sysdig-deploy
```

## Installation with Proxy and Custom Image Repo(Internal Registry)
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)>
--set global.proxy.httpProxy=<Http Proxy> \
--set global.proxy.httpsProxy=<Https Proxy> \
--set global.proxy.noProxy="<No Proxy, comma delimited list>" \
--set agent.sysdig.settings.http_proxy.proxy_port=<Proxy Port> \
--set agent.sysdig.settings.http_proxy.proxy_host=<Proxy Host> \
--set agent.image.registry=<Internal Registry> \
--set agent.image.repository=<Internal Sysdig Agent Image> \
--set agent.image.pullSecrets=<Internal Registry Pull Secret> \
--set nodeAnalyzer.image.registry=<Internal Registry> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.image.repository=<Internal Sysdig Runtime Scanner Image> \
--set nodeAnalyzer.nodeAnalyzer.pullSecrets=<Internal Registry Pull Secret> \
-f static-values.yaml \
sysdig/sysdig-deploy
```

-----------------------

## Basic installation with PriorityClass
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)> \
--set agent.priorityClassName=<Priority class for agent ds, e.g: system-node-critical> \
-f static-values.yaml \
sysdig/sysdig-deploy
```

## Installation with Proxy with PriorityClass
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)>
--set global.proxy.httpProxy=<Http Proxy> \
--set global.proxy.httpsProxy=<Https Proxy> \
--set global.proxy.noProxy="<No Proxy, comma delimited list>" \
--set agent.sysdig.settings.http_proxy.proxy_port=<Proxy Port> \
--set agent.sysdig.settings.http_proxy.proxy_host=<Proxy Host> \
--set agent.priorityClassName=<Priority class for agent ds, e.g: system-node-critical> \
-f static-values.yaml \
sysdig/sysdig-deploy
```

## Installation with Proxy and Custom Image Repo(Internal Registry) with PriorityClass
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)>
--set global.proxy.httpProxy=<Http Proxy> \
--set global.proxy.httpsProxy=<Https Proxy> \
--set global.proxy.noProxy="<No Proxy, comma delimited list>" \
--set agent.sysdig.settings.http_proxy.proxy_port=<Proxy Port> \
--set agent.sysdig.settings.http_proxy.proxy_host=<Proxy Host> \
--set agent.image.registry=<Internal Registry> \
--set agent.image.repository=<Internal Sysdig Agent Image> \
--set agent.image.pullSecrets=<Internal Registry Pull Secret> \
--set nodeAnalyzer.image.registry=<Internal Registry> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.image.repository=<Internal Sysdig Runtime Scanner Image> \
--set nodeAnalyzer.nodeAnalyzer.pullSecrets=<Internal Registry Pull Secret> \
--set agent.priorityClassName=<Priority class for agent ds, e.g: system-node-critical> \
-f static-values.yaml \
sysdig/sysdig-deploy
```

-----------------------

## Basic installation with EBF enabled
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)> \
-f static-values.yaml \
sysdig/sysdig-deploy
```

## Installation with Proxy with EBF enabled
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)> \
--set global.proxy.httpProxy=<Http Proxy> \
--set global.proxy.httpsProxy=<Https Proxy> \
--set global.proxy.noProxy="<No Proxy, comma delimited list>" \
--set agent.sysdig.settings.http_proxy.proxy_port=<Proxy Port> \
--set agent.sysdig.settings.http_proxy.proxy_host=<Proxy Host> \
--set agent.ebpf.enabled=true \
-f static-values.yaml \
sysdig/sysdig-deploy
```

## Installation with Proxy and Custom Image Repo(Internal Registry) with EBF enabled
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)> \
--set global.proxy.httpProxy=<Http Proxy> \
--set global.proxy.httpsProxy=<Https Proxy> \
--set global.proxy.noProxy="<No Proxy, comma delimited list>" \
--set agent.sysdig.settings.http_proxy.proxy_port=<Proxy Port> \
--set agent.sysdig.settings.http_proxy.proxy_host=<Proxy Host> \
--set agent.image.registry=<Internal Registry> \
--set agent.image.repository=<Internal Sysdig Agent Image> \
--set agent.image.pullSecrets=<Internal Registry Pull Secret> \
--set nodeAnalyzer.image.registry=<Internal Registry> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.image.repository=<Internal Sysdig Runtime Scanner Image> \
--set nodeAnalyzer.nodeAnalyzer.pullSecrets=<Internal Registry Pull Secret> \
--set agent.ebpf.enabled=true \
-f static-values.yaml \
sysdig/sysdig-deploy
```

--------------------------------
## For images running in your cluster that are larger than 2GB, include the following configurations with largest size of image in your cluster:

## You can find largest image size by running this command:
```
kubectl get nodes -o json | jq -r '.items[].status.images[] | .sizeBytes' | sort -nr | head -1
```

## If modifying maxImageSizeAllowed, please also adjust ephemeral storage following below format to accommodate large image:

* The ephemeral storage request for the sysdig vuln-runtime-scanner should be set to 2Gi (the default) or 1.5 times the size of the largest image on the cluster, whichever is greater


## Basic installation with maxImageSize and ephemeralStorage Increase
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.settings.maxImageSizeAllowed=<largest image size> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.resources.requests.ephemeral-storage=<storage size request in bytes> \
-f static-values.yaml \
sysdig/sysdig-deploy
```

## Installation with Proxy with maxImageSize and ephemeralStorage Increase
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)> \
--set global.proxy.httpProxy=<Http Proxy> \
--set global.proxy.httpsProxy=<Https Proxy> \
--set global.proxy.noProxy="<No Proxy, comma delimited list>" \
--set agent.sysdig.settings.http_proxy.proxy_port=<Proxy Port> \
--set agent.sysdig.settings.http_proxy.proxy_host=<Proxy Host> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.settings.maxImageSizeAllowed=<largest image size> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.resources.requests.ephemeral-storage=<storage size request in bytes> \
-f static-values.yaml \
sysdig/sysdig-deploy
```

## Installation with Proxy and Custom Image Repo(Internal Registry) with maxImageSize and ephemeralStorage Increase
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)> \
--set global.proxy.httpProxy=<Http Proxy> \
--set global.proxy.httpsProxy=<Https Proxy> \
--set global.proxy.noProxy="<No Proxy, comma delimited list>" \
--set agent.sysdig.settings.http_proxy.proxy_port=<Proxy Port> \
--set agent.sysdig.settings.http_proxy.proxy_host=<Proxy Host> \
--set agent.image.registry=<Internal Registry> \
--set agent.image.repository=<Internal Sysdig Agent Image> \
--set agent.image.pullSecrets=<Internal Registry Pull Secret> \
--set nodeAnalyzer.image.registry=<Internal Registry> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.image.repository=<Internal Sysdig Runtime Scanner Image> \
--set nodeAnalyzer.nodeAnalyzer.pullSecrets=<Internal Registry Pull Secret> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.settings.maxImageSizeAllowed=<largest image size> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.resources.requests.ephemeral-storage=<storage size request in bytes> \
-f static-values.yaml \
sysdig/sysdig-deploy
```

--------------------------------
## For images running in your cluster that are larger than 2GB, include the following configurations with largest size of image in your cluster:

## You can find largest image size by running this command:
```
kubectl get nodes -o json | jq -r '.items[].status.images[] | .sizeBytes' | sort -nr | head -1
```

## If modifying maxImageSizeAllowed, please also adjust ephemeral storage following below format to accommodate large image:

* The ephemeral storage request for the sysdig vuln-runtime-scanner should be set to 2Gi (the default) or 1.5 times the size of the largest image on the cluster, whichever is greater


## Basic installation with maxImageSize and ephemeralStorage Increase and EBF enabled
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.settings.maxImageSizeAllowed=<largest image size> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.resources.requests.ephemeral-storage=<storage size request in bytes> \
--set agent.ebpf.enabled=true \
-f static-values.yaml \
sysdig/sysdig-deploy
```

## Installation with Proxy with maxImageSize and ephemeralStorage Increase and EBF enabled
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)> \
--set global.proxy.httpProxy=<Http Proxy> \
--set global.proxy.httpsProxy=<Https Proxy> \
--set global.proxy.noProxy="<No Proxy, comma delimited list>" \
--set agent.sysdig.settings.http_proxy.proxy_port=<Proxy Port> \
--set agent.sysdig.settings.http_proxy.proxy_host=<Proxy Host> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.settings.maxImageSizeAllowed=<largest image size> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.resources.requests.ephemeral-storage=<storage size request in bytes> \
--set agent.ebpf.enabled=true \
-f static-values.yaml \
sysdig/sysdig-deploy
```

## Installation with Proxy and Custom Image Repo(Internal Registry) with maxImageSize and ephemeralStorage Increase and EBF enabled
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)> \
--set global.proxy.httpProxy=<Http Proxy> \
--set global.proxy.httpsProxy=<Https Proxy> \
--set global.proxy.noProxy="<No Proxy, comma delimited list>" \
--set agent.sysdig.settings.http_proxy.proxy_port=<Proxy Port> \
--set agent.sysdig.settings.http_proxy.proxy_host=<Proxy Host> \
--set agent.image.registry=<Internal Registry> \
--set agent.image.repository=<Internal Sysdig Agent Image> \
--set agent.image.pullSecrets=<Internal Registry Pull Secret> \
--set nodeAnalyzer.image.registry=<Internal Registry> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.image.repository=<Internal Sysdig Runtime Scanner Image> \
--set nodeAnalyzer.nodeAnalyzer.pullSecrets=<Internal Registry Pull Secret> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.settings.maxImageSizeAllowed=<largest image size> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.resources.requests.ephemeral-storage=<storage size request in bytes> \
--set agent.ebpf.enabled=true \
-f static-values.yaml \
sysdig/sysdig-deploy
```

--------------------------------
## For images running in your cluster that are larger than 2GB, include the following configurations with largest size of image in your cluster:

## You can find largest image size by running this command:
```
kubectl get nodes -o json | jq -r '.items[].status.images[] | .sizeBytes' | sort -nr | head -1
```

## If modifying maxImageSizeAllowed, please also adjust ephemeral storage following below format to accommodate large image:

* The ephemeral storage request for the sysdig vuln-runtime-scanner should be set to 2Gi (the default) or 1.5 times the size of the largest image on the cluster, whichever is greater


## Basic installation with maxImageSize and ephemeralStorage Increase and EBF enabled and PriorityClass
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.settings.maxImageSizeAllowed=<largest image size> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.resources.requests.ephemeral-storage=<storage size request in bytes> \
--set agent.ebpf.enabled=true \
--set agent.priorityClassName=<Priority class for agent ds, e.g: system-node-critical> \
-f static-values.yaml \
sysdig/sysdig-deploy
```

## Installation with Proxy with maxImageSize and ephemeralStorage Increase and EBF enabled and PriorityClass
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)> \
--set global.proxy.httpProxy=<Http Proxy> \
--set global.proxy.httpsProxy=<Https Proxy> \
--set global.proxy.noProxy="<No Proxy, comma delimited list>" \
--set agent.sysdig.settings.http_proxy.proxy_port=<Proxy Port> \
--set agent.sysdig.settings.http_proxy.proxy_host=<Proxy Host> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.settings.maxImageSizeAllowed=<largest image size> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.resources.requests.ephemeral-storage=<storage size request in bytes> \
--set agent.ebpf.enabled=true \
--set agent.priorityClassName=<Priority class for agent ds, e.g: system-node-critical> \
-f static-values.yaml \
sysdig/sysdig-deploy
```

## Installation with Proxy and Custom Image Repo(Internal Registry) with maxImageSize and ephemeralStorage Increase and EBF enabled and PriorityClass
```
helm repo add sysdig https://charts.sysdig.com

helm repo update

helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)> \
--set global.proxy.httpProxy=<Http Proxy> \
--set global.proxy.httpsProxy=<Https Proxy> \
--set global.proxy.noProxy="<No Proxy, comma delimited list>" \
--set agent.sysdig.settings.http_proxy.proxy_port=<Proxy Port> \
--set agent.sysdig.settings.http_proxy.proxy_host=<Proxy Host> \
--set agent.image.registry=<Internal Registry> \
--set agent.image.repository=<Internal Sysdig Agent Image> \
--set agent.image.pullSecrets=<Internal Registry Pull Secret> \
--set nodeAnalyzer.image.registry=<Internal Registry> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.image.repository=<Internal Sysdig Runtime Scanner Image> \
--set nodeAnalyzer.nodeAnalyzer.pullSecrets=<Internal Registry Pull Secret> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.settings.maxImageSizeAllowed=<largest image size> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.resources.requests.ephemeral-storage=<storage size request in bytes> \
--set agent.ebpf.enabled=true \
--set agent.priorityClassName=<Priority class for agent ds, e.g: system-node-critical> \
-f static-values.yaml \
sysdig/sysdig-deploy
```





# Additional Configurations

## If using internal image registry, include below configurations:
```
--set agent.image.registry=<Internal Registry> \
--set agent.image.repository=<Internal Sysdig Agent Image> \
--set agent.image.pullSecrets=<Internal Registry Pull Secret> \
--set nodeAnalyzer.image.registry=<Internal Registry> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.image.repository=<Internal Sysdig Runtime Scanner Image> \
--set nodeAnalyzer.nodeAnalyzer.pullSecrets=<Internal Registry Pull Secret> \
```

## To override image tag for agent and runtime scanner, add following configurations with specific versions:
```
--set agent.image.tag=<Sysdig Agent Tag> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.image.tag=<Sysdig Runtime Scanner Tag> \
```

## For images running in your cluster that are larger than 2GB, include the following configurations with largest size of image in your cluster:
```
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.settings.maxImageSizeAllowed=<largest image size> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.resources.requests.ephemeral-storage=<storage size request in bytes> \
```
## You can find largest image size by running this command:
```
kubectl get nodes -o json | jq -r '.items[].status.images[] | .sizeBytes' | sort -nr | head -1
```

## If modifying maxImageSizeAllowed, please also adjust ephemeral storage following below format to accommodate large image:

* The ephemeral storage request for the sysdig vuln-runtime-scanner should be set to 2Gi (the default) or 1.5 times the size of the largest image on the cluster, whichever is greater
```
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.resources.requests.ephemeral-storage=<storage size request in bytes> \
```
## If SElinux or Secure Boot is enabled, add the following configuration(not very common):
```
--set agent.ebpf.enabled=true \
```
