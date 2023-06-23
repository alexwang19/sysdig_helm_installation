## Sysdig Installation Steps

1. ```helm repo add sysdig https://charts.sysdig.com```

2. ```helm repo update```

4. ```
helm install sysdig-agent --namespace <namespace where sysdig components will be deployed> \
--set global.sysdig.accessKey=<Agent Access Key> \
--set global.clusterConfig.name=<Cluster Name> \
--set global.sysdig.region=<Sysdig Region(default us3)>
--set global.proxy.httpProxy=<Http Proxy> \
--set global.proxy.httpsProxy=<Https Proxy> \
--set global.proxy.noProxy="<No Proxy>" \
--set agent.image.tag=<Sysdig Agent Tag> \
--set agent.sysdig.settings.http_proxy.proxy_port=<Proxy Port> \
--set agent.sysdig.settings.http_proxy.proxy_host=<Proxy Host> \
--set agent.priorityClassName=<Priority class for agent ds, REMOVE IF NOT REQUIRED>
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.image.tag=<Sysdig Runtime Scanner Tag> \
sysdig/sysdig-deploy
```


# Additional Configurations

## If using internal image registry, include below parameters:
```
--set agent.image.registry=<Internal Registry> \
--set agent.image.repository=<Internal Sysdig Agent Image> \
--set agent.image.pullSecrets=<Internal Registry Pull Secret> \
--set nodeAnalyzer.image.registry=<Internal Registry> \
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.image.repository=<Internal Sysdig Runtime Scanner Image, REMOVE IF NOT USING INTERNAL REGISTRY> \
--set nodeAnalyzer.nodeAnalyzer.pullSecrets=<Internal Registry Pull Secret, REMOVE IF NOT USING INTERNAL REGISTRY> \
```

## For images running in your cluster that are larger than 2GB, include the following parameter with largest size of image in your cluster:
```
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.settings.maxImageSizeAllowed=<largest image size> \
```
## You can find largest image size by running this command:
```
kubectl get nodes -o json | jq -r '.items[].status.images[] | .sizeBytes' | sort -nr | head -1
```

## If modifying maxImageSize, please also adjust ephemeral storage following below formal to accommodate large image:

* The ephemeral storage request for the sysdig vuln-runtime-scanner should be set to 2Gi (the default) or 1.5 times the size of the largest image on the cluster, whichever is greater
```
--set nodeAnalyzer.nodeAnalyzer.runtimeScanner.resources.requests.ephemeral-storage=<storage size request in bytes> \
```
## If SElinux or Secure Boot is enabled, add the following setting(not very common):
```
--set agent.ebpf.enabled=true \
```