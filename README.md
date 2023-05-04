# kubeinvaders-Istio-Datadog

Installing kubeinvaders

helm repo add kubeinvaders https://lucky-sideburn.github.io/helm-charts/
helm repo update

kubectl create namespace kubeinvaders

helm install kubeinvaders -f invaders_values.yaml --set-string config.target_namespace="kube-system" \
-n kubeinvaders kubeinvaders/kubeinvaders --set ingress.enabled=true --set ingress.hostName=kubeinvaders.io --set deployment.image.tag=v1.9.6

helm upgrade kubeinvaders -f invaders_values.yaml -n kubeinvaders kubeinvaders/kubeinvaders --set ingress.enabled=true --set ingress.hostName=kubeinvaders.io --set deployment.image.tag=v1.9.6

1. Installing istio with helm: https://istio.io/latest/docs/setup/install/helm/ 

helm repo add istio.io https://storage.googleapis.com/istio-release/releases/1.1.7/charts/ 

helm repo list 

helm install istio-base istio/base -n istio-system --create-namespace 

helm install istiod istio/istiod -n istio-system --wait

kubectl get deployments -n istio-system --output wide 

3.  helm install istio-ingress istio/gateway -n istio-ingress --create-namespace --wait 

kubectl label namespace kubeinvaders istio-injection=enabled 


1. helm install datadog-v1 -f dd_values.yaml  --set datadog.apiKey=$DD_API_KEY datadog/datadog --set targetSystem=linux -n monitoring --create-namespace --wait
