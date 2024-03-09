# GKE SpringBoot MicroService Helm Chart

Repository created to store the Helm Chart objects & config. files needed to deploy My REST-API App on GCP GKE Service.

## Helm Version

The Helm version used to install the Service is:

* **version.BuildInfo{Version:"v3.9.1" ... GoVersion:"go1.17.5"}**

## Helm main components used in My REST-API Service

* **Chart.yaml:** Main Helm Chart file, contains info. about the Helm Chart / Package & the embedded application. version & appVersion tags should be validated & updated (if needed) constantly before deployment to GKE (or any other k8s engine service).
* **templates/:** Folder than contains templates of the k8s objects that are installed within GKE, for My REST-API Service deployment.yaml & service.yaml were relevant to deploy the Service on MH GKE Clusters.
* **values.yaml:** This file is used to override values on the templates & change the behavior of the k8s objects installed on the GKE Clusters.

## Helm basic commands

Command to validate version:

```
helm version
```

Command to validate where was helm installed:

```
which helm
```

Command to create a Helm Chart (folder with Helm components):

```
helm create "<CHART_NAME>"
```

Command to install the Chart / Package with embedded application within GKE Cluster:

**Note:** Image tag of the container image within Quay is set via --set image.tag & Cluster namespace is set via --namespace. The best approach / practice is to use "helm upgrade ..." command.

```
helm install --set image.tag="<IMAGE_TAG>" --namespace "<CLUSTER_NAMESPACE>" "<CHART_NAME>" "<CHART_FOLDER>"/ --values "<CHART_FOLDER>"/values.yaml
```

Command to install (if not exists) / upgrade (if exists) a Helm Chart / Package:

**Note:** This command was used on the deployment Jenkins Jobs created for My REST-API Service.

```
helm upgrade --install --set image.tag="<IMAGE_TAG>" --namespace "<CLUSTER_NAMESPACE>" "<CHART_NAME>" "<CHART_FOLDER>" --values "<CHART_FOLDER>"/values.yaml
```

Command to validate the Helm Chart was installed:

```
helm list --namespace "<CLUSTER_NAMESPACE>"
```

Command to validate the status of a Helm Chart installed:

```
helm status "<CHART_NAME>"
```

Command to delete a installed / running Helm Chart:

```
helm delete "<CHART_NAME>" --namespace "<CLUSTER_NAMESPACE>"
```
