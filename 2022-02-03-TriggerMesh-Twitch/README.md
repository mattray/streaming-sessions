# TriggerMesh Twitch

[twitch.tv/triggermesh](https://twitch.tv/triggermesh)

Rough outline:
 * Install Knative on K3s
   local Debian 11 machine called `yancy`
 * Install on vanilla 1.21 EKS
 * Install [Knative](https://knative.dev/docs/install/)
 * Install [TriggerMesh](https://docs.triggermesh.io/guides/installation/)
 * [gtflp](https://github.com/JeffNeff/gtflp) for viewing events with [config](config/gtflp-release.yaml)
 * [IBM MQ server](config/mq-server.yaml)
   * You should be able to access the MQ Server at https://localhost:9443/ibmmq/console/ accept the certificate, and login with the user `admin` and password `passw0rd`.
 * [MQ source](config/mq-source.yaml)

## Commands

These are the (sanitized) commands used during the session.
```
aws eks update-kubeconfig --region ap-southeast-2 --name livestream
kubectx
kubens
kubectl get nodes
export KUBECONFIG=/Users/mattray/.kube/yancy-k3s.yaml
kubectl get nodes
kubectl apply -f https://github.com/knative/serving/releases/download/knative-v1.2.0/serving-crds.yaml
kubectl apply -f https://github.com/knative/serving/releases/download/knative-v1.2.0/serving-core.yaml
kubectl apply -f https://github.com/knative/net-kourier/releases/download/knative-v1.2.0/kourier.yaml
kubectl patch configmap/config-network --namespace knative-serving --type merge --patch '{"data":{"ingress.class":"kourier.ingress.networking.knative.dev"}}'
kubectl --namespace kourier-system get service kourier
kubectl get pods -n knative-serving
kubectl apply -f https://github.com/knative/serving/releases/download/knative-v1.2.0/serving-default-domain.yaml
kubectl apply -f https://github.com/knative/eventing/releases/download/knative-v1.2.0/eventing-crds.yaml
kubectl apply -f https://github.com/knative/eventing/releases/download/knative-v1.2.0/eventing-core.yaml
kubectl get pods -n knative-eventing
kubectl apply -f https://github.com/triggermesh/triggermesh/releases/latest/download/triggermesh-crds.yaml
kubectl apply -f https://github.com/triggermesh/triggermesh/releases/latest/download/triggermesh.yaml
kubectl get pods -n triggermesh
kubectl get crds |grep triggermesh |grep aws
kubectl get crds |grep triggermesh |grep aws| wc
kubectl get crds |grep triggermesh
kubectl get crds |grep triggermesh | sort
cd triggermesh/streaming-sessions/2022-02-03-TriggerMesh-Twitch
kubectl apply -f config/gtflp-release.yaml
kubectl get ksvc
kubectl apply -f config/mq-server.yaml
kubectl apply -f config/gtflp-release.yaml
kubectl port-forward deployments/ibm-mq-server 9443 &
```
