# A word on grafana
To do

# Create grafana repo
As stated on [platform-apps](), I prefer to play as **All the artifacts are under my organization scope**. This means, I don´t install nothing from source repo. The procedure is to downlado the new version, update the `index.yaml` and then install.

## Create or update repo
This is only to download the last artifact.
```bash
helm repo add grafana https://grafana.github.io/helm-charts ; helm repo update grafana
helm search repo grafana/grafana
helm pull grafana/grafana -d ../
helm repo index ../
```
Merge this changes on main. Now, 
```bash
helm repo add platform-observability https://publicstaticdevnull.github.io/platform-observability ; helm repo update platform-observabilitys
helm search repo platform-observability     # To check everything went well
```
If you want to try it manually, follow. 


## Install Manually
Just for kicks. This is intalled through ArgoCD.

```bash
helm install grafana platform-observability/grafana \
--namespace monitoring \
--create-namespace=true \
-f values.yaml --rollback-on-failure
```

# A word on Minikube

The StoragClass is retrieved by
```bash
k get staorageclass
```
But for kickstart. The idea is to use a PV / PVC... I know it's useless, but for kickstart. To work it out well, Must be done using a postgreSQL.