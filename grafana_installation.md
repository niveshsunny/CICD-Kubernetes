# Install using Helm

## Add helm repo

`helm repo add grafana https://grafana.github.io/helm-charts`

## Update helm repo

`helm repo update`

## Install helm 

`helm install grafana grafana/grafana`

## Expose Grafana Service with type LoadBalancer
## decode passwords using bas64 , username: admin
`kubectl expose service grafana — type=LoadBalancer — target-port=3000 — name=grafana-ext`
