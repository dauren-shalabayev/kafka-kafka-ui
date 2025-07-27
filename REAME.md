curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update

export KUBECONFIG=/etc/rancher/k3s/k3s.yaml


kubectl get nodes

sudo KUBECONFIG=/etc/rancher/k3s/k3s.yaml helm install kafka bitnami/kafka \
  --set replicas=1 \
  --set zookeeper.replicaCount=1 \
  --set resources.requests.memory=512Mi \
  --set resources.limits.memory=1Gi \
  --set zookeeper.resources.requests.memory=256Mi \
  --set zookeeper.resources.limits.memory=512Mi


kubectl get pods -l app.kubernetes.io/name=kafka


kubectl apply -f kafka-ui-deploy.yaml
