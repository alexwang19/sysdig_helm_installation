# Sysdig Installation Steps


## START HERE

### Quick Start Questionnaire

<p>Please answer these questions and record answers in following format (1.(answer),2.(answer),3.(answer),4.(answer),5.(answer)). You can then use Ctrl+F or CMD+F to find appropriate install option with that answer format.
example:(1.Yes,2.No,3.No,4.Yes,5.No)
</p>

1. Do you need proxy enabled?
2. Are you using a custom image repo (internal registry)?
3. Do you have SELinux or Secure Boot enabled(not common)?
4. Do you need to specify a priority class(e.g. system-node-critical)?
5. Is the largest image running in your cluster larger than 2GB?
- You can find largest image size by running this command:
```
kubectl get nodes -o json | jq -r '.items[].status.images[] | .sizeBytes' | sort -nr | head -1
```

### Options Available

* [Install with proxy](#installation-with-proxy)
* [Installation with Proxy and Custom Image Repo(Internal Registry)](#installation-with-proxy-and-custom-image-repointernal-registry)
* [Basic installation with PriorityClass](#basic-installation-with-priorityclass)
* [Installation with Proxy with PriorityClass](#installation-with-proxy-with-priorityclass)
* [Installation with Proxy and Custom Image Repo(Internal Registry) with PriorityClass](#installation-with-proxy-and-custom-image-repointernal-registry-with-priority-class)
* [Basic installation with EBF enabled](#basic-installation-with-ebf-enabled)
* [Installation with Proxy with EBF enabled](#installation-with-proxy-with-ebf-enabled)
* [Installation with Proxy and Custom Image Repo(Internal Registry) with EBF enabled](#installation-with-proxy-and-custom-image-repointernal-registry-with-ebf-enabled)
* [Basic installation with maxImageSize and ephemeralStorage Increase](#basic-installation-with-maximagesize-and-ephemeralstorage-increase)
* [Installation with Proxy with maxImageSize and ephemeralStorage Increase](#installation-with-proxy-with-maximagesize-and-ephemeralstorage-increase)
* [Installation with Proxy and Custom Image Repo(Internal Registry) with maxImageSize and ephemeralStorage Increase](#installation-with-proxy-and-custom-image-repointernal-registry-with-maximagesize-and-ephemeralstorage-increase)
* [Basic installation with maxImageSize and ephemeralStorage Increase and EBF enabled](#basic-installation-with-maximagesize-and-ephemeralstorage-increase-and-ebf-enabled)
* [Installation with Proxy with maxImageSize and ephemeralStorage Increase and EBF enabled](#installation-with-proxy-with-maximagesize-and-ephemeralstorage-increase-and-ebf-enabled)
* [Installation with Proxy and Custom Image Repo(Internal Registry) with maxImageSize and ephemeralStorage Increase and EBF enabled](#installation-with-proxy-and-custom-image-repointernal-registry-with-maximagesize-and-ephemeralstorage-increase-and-ebf-enabled)
* [Basic installation with maxImageSize and ephemeralStorage Increase and EBF enabled and PriorityClass](#basic-installation-with-maximagesize-and-ephemeralstorage-increase-and-ebf-enabled-and-priorityclass)
* [Installation with Proxy with maxImageSize and ephemeralStorage Increase and EBF enabled and PriorityClass](#installation-with-proxy-with-maximagesize-and-ephemeralstorage-increase-and-ebf-enabled-and-priorityclass)
* [Installation with Proxy and Custom Image Repo(Internal Registry) with maxImageSize and ephemeralStorage Increase and EBF enabled and PriorityClass](#installation-with-proxy-and-custom-image-repointernal-registry-with-maximagesize-and-ephemeralstorage-increase-and-ebf-enabled-and-priorityclass)

-------------------------------------

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
