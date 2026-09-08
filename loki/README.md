# A word on grafana
To do

# Create loki repo
As stated on [platform-apps](), I prefer to play as **All the artifacts are under my organization scope**. This means, I don´t install nothing from source repo. The procedure is to downlado the new version, update the `index.yaml` and then install.

## Create or update repo
This is only to download the last artifact.
```bash
helm repo add grafana https://grafana.github.io/helm-charts ; helm repo update grafana
helm search repo grafana/loki
helm pull grafana/loki -d ../
helm repo index ../
```
Merge this changes on main. Now, 



## Install Manually
Just for kicks. This is intalled through ArgoCD.

```bash
cd loki
htpasswd -c .htpasswd loki
kubectl create secret generic loki-basic-auth --from-file=.htpasswd -n monitoring
kubectl create secret generic canary-basic-auth --from-literal=username=loki --from-literal=password=1234 -n monitoring 

helm install loki grafana/loki \
--namespace monitoring \
--create-namespace=true \
-f values.yaml --rollback-on-failure
```

# A word on htpasswd
The username and password is **ON PURPOSE** on plain text. No way I'm doing this in production. Yes a later step is to grab the password from a secret manager and create the httpasswd using a pipeline. 

# A word on Minikube

The StoragClass is retrieved by
```bash
k get staorageclass
```
But for kickstart. The idea is to use a PV / PVC... I know it's useless, but for kickstart. To work it out well, must be done using a postgreSQL to persistent save of the configuration