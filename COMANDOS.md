# 🧭 Comandos útiles de Minikube y Kubernetes

Este documento recopila los comandos más comunes y útiles para trabajar con **Minikube** y **Kubernetes**.  
Ideal para tener como referencia rápida o incluir en tu portafolio.

---

## 🚀 Minikube

| Comando | Descripción |
|----------|--------------|
| `minikube service <service_name>` | Expone el servicio por un puerto para accederlo |
| `minikube image ls` | Muestra el listado de imágenes |
| `minikube image load <image_local>` | Carga una imagen local a las imágenes de Minikube |
| `minikube dashboard` | Muestra un dashboard con Pods, Deployments, Services y más |
| `minikube start --vm-driver=none --extra-config=apiserver.authorization-mode=RBAC` | Habilita RBAC |
| `minikube addons enable ingress` | Habilita un ingress en Minikube con nginx |
| `minikube service ingress-nginx-controller --url -n ingress-nginx` | Permite acceder al servicio del nginx |

---

## ☸️ Comandos de Kubernetes

### 🧩 Pods

| Comando | Descripción |
|----------|--------------|
| `k run <name_pod> --image=nginx --port=80` | Crea un pod |
| `k get pods` | Lista los pods |
| `k apply -f pod.yml` | Aplica el manifiesto |
| `k get pods -l app=nginx` | Lista pods con un label |
| `k delete pod <name_pod>` | Elimina un pod |
| `k logs -f <name_pod>` | Muestra logs del pod |
| `k port-forward <name_pod> <mi_puerto:puerto_pod>` | Redirige un puerto |
| `k describe <name_pod>` | Información detallada del pod |
| `k api-versions` | Muestra las versiones de la API |
| `k api-resources` | Muestra los recursos disponibles |
| `k label pods <mi_pod> app=pod-label` | Añade label a un pod existente |
| `k get pod <name_pod> -o yaml` | Muestra información YAML del pod |
| `k edit <resource> <name>` | Edita configuración del recurso en vivo |

---

### 🔁 ReplicaSet

| Comando | Descripción |
|----------|--------------|
| `k get replicasets` | Lista los ReplicaSets |
| `k describe rs <rs_name>` | Describe un ReplicaSet |

---

### ⚙️ Deployment

| Comando | Descripción |
|----------|--------------|
| `k get deployments` | Lista los deployments |
| `k get deployments --show-labels` | Muestra los labels de los deployments |
| `k rollout status deployment <name>` | Muestra el estado del rollout |
| `k rollout history deployment <name>` | Muestra el historial de cambios |
| `k apply -f deployment.yml --record` | Aplica y guarda el historial (deprecated) |
| `k rollout history deployment <name> --revision=<rev>` | Muestra una revisión específica |
| `k rollout undo deployment <name> --to-revision=<rev>` | Hace rollback a una versión anterior |
| `k get deploy -n <ns> <name> -o yaml` | Muestra el YAML del deployment |

---

### 🌐 Service

| Comando | Descripción |
|----------|--------------|
| `k get svc` | Lista los servicios |
| `k get svc -l app=<label>` | Lista los servicios con un label |
| `k describe svc -l app=nginx` | Describe un servicio |
| `k get endpoints` | Lista los endpoints (deprecated) |
| `k describe endpoints <svc_name>` | Describe los endpoints del servicio |

---

### 🧭 Namespace

| Comando | Descripción |
|----------|--------------|
| `k get ns` | Lista los namespaces |
| `k get pods -n <namespace>` | Lista los pods de un namespace |
| `k get all -n <namespace>` | Muestra todos los recursos de un namespace |
| `k create namespace <namespace>` | Crea un namespace |
| `k describe ns <namespace>` | Describe un namespace |
| `k run prueba --image=nginx -n <namespace>` | Crea un pod en un namespace |
| `k delete pod <name> -n <namespace>` | Elimina un pod de un namespace |
| `k delete ns <namespace>` | Elimina un namespace |

---

### ⚙️ Contextos

| Comando | Descripción |
|----------|--------------|
| `k config current-context` | Muestra el contexto actual |
| `k config view` | Muestra la configuración |
| `k config set-context ci-context --namespace=ci --cluster=minikube --user=minikube` | Crea un contexto |
| `k config use-context ci-context` | Cambia el contexto |
| `k config get-contexts` | Lista los contextos disponibles |

---

### 🔒 LimitRange

| Comando | Descripción |
|----------|--------------|
| `k get limitrange -n <namespace>` | Lista los limit ranges |
| `k describe limits <name> -n <namespace>` | Describe un limit range |

---

### 💾 ResourceQuota

| Comando | Descripción |
|----------|--------------|
| `k get quota -n <namespace>` | Lista los ResourceQuotas |
| `k describe quota <name> -n <namespace>` | Describe un ResourceQuota |

---

### ⚙️ ConfigMaps

| Comando | Descripción |
|----------|--------------|
| `k create configmap <name> --from-file=path/to/file` | Crea un ConfigMap |
| `k get cm` | Lista los ConfigMaps |
| `k describe cm <name>` | Describe un ConfigMap |
| `k create configmap <name> --from-file=path/to/folder` | Crea un ConfigMap con varios archivos |

---

### 🔑 Secrets

| Comando | Descripción |
|----------|--------------|
| `k create secret generic <name> --from-file=path/to/file` | Crea un secreto |
| `k get secrets` | Lista los secretos |
| `k describe secret <name>` | Describe un secreto |
| `k get secrets -o yaml` | Muestra secretos en formato YAML (base64) |

---

### 💽 Volúmenes

| Comando | Descripción |
|----------|--------------|
| `k get pv` | Lista los PersistentVolumes |
| `k describe pv <name>` | Describe un PersistentVolume |
| `k get pvc` | Lista los PersistentVolumeClaims |
| `k describe pvc <name>` | Describe un PersistentVolumeClaim |
| `k get sc` | Lista las StorageClasses |

---

### 🔐 RBAC (Autenticación y Autorización)

| Comando | Descripción |
|----------|--------------|
| `k cluster-info` | Muestra información del clúster |
| `k config view` | Muestra la configuración actual |
| `k cluster-info dump | grep authorization-mode` | Verifica si RBAC está habilitado |
| `k get roles` | Lista los roles creados |
| `k describe role <name>` | Describe un rol |
| `k get rolebinding` | Lista los rolebindings |
| `k describe rolebinding <name>` | Describe un rolebinding |
| `k get clusterroles` | Lista los cluster roles |
| `k get clusterrolebindings` | Lista los cluster role bindings |

---

### 🧰 Service Accounts

| Comando | Descripción |
|----------|--------------|
| `k get sa` | Lista las service accounts |
| `k describe sa <name>` | Describe una service account |
| `TOKEN=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token)` | Guarda el token actual |
| `curl -H "Authorization: Bearer ${TOKEN}" https://kubernetes/api/v1 --insecure` | Verifica acceso a la API |
| `curl -H "Authorization: Bearer ${TOKEN}" https://kubernetes/api/v1/namespaces/default/pods --insecure` | Lista pods desde la API |

---
## ☁️ Kubernetes en AWS (EKS)

### Instalación y configuración de EKS

| Comando | Descripción |
|--------|-------------|
| `eksctl create cluster --name test-cluster --region us-east-1 --zones us-east-1a,us-east-1b --without-nodegroup --profile dev` | Crea un clúster EKS en AWS (usando el profile `dev`) |
| `aws eks --region us-east-1 update-kubeconfig --name <cluster_name>` | Configura el archivo kubeconfig para conectarse al clúster |
| `eksctl create nodegroup --region us-east-1 --cluster=test-cluster --name=test-workers --node-type=t3.medium --nodes=1 --nodes-min=1 --nodes-max=3 --asg-access --spot --profile dev` | Agrega un grupo de nodos al clúster |

---

### Asociar OIDC y Load Balancer

| Comando | Descripción |
|--------|-------------|
| `eksctl utils associate-iam-oidc-provider --region us-east-1 --cluster test-cluster --approve --profile dev` | Asocia un OIDC provider al clúster |
| `curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.13.3/docs/install/iam_policy.json` | Descarga la política IAM para el Load Balancer Controller |
| `aws iam create-policy --policy-name AWSLoadBalancerControllerIAMPolicy --policy-document file://iam_policy.json --profile dev` | Crea la política IAM en AWS |
| `eksctl create iamserviceaccount --cluster=test-cluster --namespace=kube-system --name=aws-load-balancer-controller --role-name AmazonEKSLoadBalancerControllerRole --attach-policy-arn=arn:aws:iam::<AWS_ACCOUNT_ID>:policy/AWSLoadBalancerControllerIAMPolicy --approve --region us-east-1 --profile dev` | Crea la service account para el Load Balancer Controller |

---

### Despliegue del AWS Load Balancer Controller

```bash
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.13.5/cert-manager.yaml
curl -Lo v2_13_3_full.yaml https://github.com/kubernetes-sigs/aws-load-balancer-controller/releases/download/v2.13.3/v2_13_3_full.yaml
sed -i.bak -e '730,738d' ./v2_13_3_full.yaml
sed -i.bak -e 's|your-cluster-name|test-cluster|' ./v2_13_3_full.yaml
kubectl apply -f v2_13_3_full.yaml
curl -Lo v2_13_3_ingclass.yaml https://github.com/kubernetes-sigs/aws-load-balancer-controller/releases/download/v2.13.3/v2_13_3_ingclass.yaml
kubectl apply -f v2_13_3_ingclass.yaml
kubectl get deployment -n kube-system aws-load-balancer-controller
```

---

### Desplegar aplicación de ejemplo

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.13.3/docs/examples/2048/2048_full.yaml
kubectl get pods -n game-2048
kubectl port-forward <pod-name> 7000:80 -n game-2048
kubectl get ing -n game-2048
```

---

### Borrar aplicación

```bash
kubectl delete -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.11.0/docs/examples/2048/2048_full.yaml
kubectl delete -f 2048_full.yaml
```

---

### HPA (Horizontal Pod Autoscaler)

| Comando | Descripción |
|--------|-------------|
| `kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.8.0/components.yaml` | Instala el metrics-server |
| `kubectl get deployment metrics-server -n kube-system` | Verifica el metrics-server |
| `kubectl top nodes` | Muestra métricas de los nodos |
| `kubectl create deployment httpd --image=httpd` | Crea un deployment de prueba |
| `kubectl set resources deployment httpd -c=httpd --limits=cpu=500m` | Configura límites de CPU |
| `kubectl expose deployment httpd --port=80` | Expone el servicio |
| `kubectl autoscale deployment httpd --cpu-percent=50 --min=2 --max=10` | Crea el HPA (escala si CPU > 50%) |
| `kubectl get hpa` | Lista los HPA creados |
| `kubectl run apache-bench -i --tty --rm --image=httpd -- bash` | Crea un pod para pruebas de carga |
| `ab -n 500000 -c 1000 http://httpd.default.svc.cluster.local/` | Ejecuta prueba de carga dentro del pod |

---

### Cluster Autoscaler (Autoescalado de nodos)

| Comando | Descripción |
|--------|-------------|
| `kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/refs/heads/master/cluster-autoscaler/cloudprovider/aws/examples/cluster-autoscaler-autodiscover.yaml` | Instala el Cluster Autoscaler |
| `kubectl edit deploy cluster-autoscaler -n kube-system` | Edita la configuración del autoscaler |
| `kubectl get pods -n kube-system` | Verifica el autoscaler |
| `kubectl logs -f <pod-name> -n kube-system` | Ver logs del autoscaler |

**Notas de configuración:**
- Agrega en el deployment:
  - `--balance-similar-node-groups`
  - `--skip-nodes-with-system-pods=false`
  - Cambia el nombre del clúster en:
    `--node-group-auto-discovery=asg:tag=k8s.io/cluster-autoscaler/enabled,k8s.io/cluster-autoscaler/<YOUR_CLUSTER_NAME>`

---

✅ **Tip**: Usa este archivo como guía rápida para practicar y administrar clusters en kubernetes.
