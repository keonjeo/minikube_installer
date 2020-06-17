## How to install minikube on Ubuntu

#### Step1. Download minikube_latest_installation package

download the package from offical website or install the package from this repository


#### Step2. Install minikube on the system

- Binary download

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

- Debian package

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
sudo dpkg -i minikube_latest_amd64.deb
```

- RPM package

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-latest.x86_64.rpm
sudo rpm -ivh minikube-latest.x86_64.rpm
```

#### Step3. Start your cluster

```bash
minikube start --image-repository=registry.cn-hangzhou.aliyuncs.com/google_containers
```

#### Step4. kubernetes阿里云的国内镜像 ( use root user to execute command )


```bash

sudo apt-get update
sudo apt-get install -y apt-transport-https curl wget
sudo curl https://mirrors.aliyun.com/kubernetes/apt/doc/apt-key.gpg | sudo  apt-key add -

cat > /etc/apt/sources.list.d/kubernetes.list << EOF
deb https://mirrors.aliyun.com/kubernetes/apt/ kubernetes-xenial main
EOF

sudo apt-get update

```

#### Step5. Install kubectl tool

```bash
sudo apt-get install -y kubectl
sudo apt-get install (kubelet kubeadm) 
```

Alternatively, minikube can download the appropriate version of kubectl, if you don’t mind the double-dashes in the command-line:

```bash
minikube kubectl -- get po -A
```

#### Step6. Interact with your cluster

```bash

kubectl get po -A
minikube kubectl -- get po -A
minikube dashboard

```

#### Step7. Deploy applications


Create a sample deployment and expose it on port 8080:

```bash

kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.4
kubectl expose deployment hello-minikube --type=NodePort --port=8080

```


It may take a moment, but your deployment will soon show up when you run:
```bash
kubectl get services hello-minikube
```


The easiest way to access this service is to let minikube launch a web browser for you:

```bash
minikube service hello-minikube
```

Alternatively, use kubectl to forward the port:

```bash
kubectl port-forward service/hello-minikube 7080:8080
```


#### Step8. Manage your cluster


Pause Kubernetes without impacting deployed applications:

```bash
minikube pause
```

Halt the cluster:

```bash
minikube pause
```


Increase the default memory limit (requires a restart):

```bash
minikube config set memory 16384
```

Browse the catalog of easily installed Kubernetes services:

```bash
minikube addons list
```

Create a second cluster running an older Kubernetes release:
```bash
minikube start -p aged --kubernetes-version=v1.16.1
```


Delete all of the minikube clusters:

```bash
minikube delete --all
```


https://blog.csdn.net/haifengid/article/details/106699850

kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.10
kubectl expose deployment hello-minikube --type=NodePort --port=8080

kubectl get pod

minikube service hello-minikube --url

minikube start --image-mirror-country=cn     --iso-url=https://kubernetes.oss-cn-hangzhou.aliyuncs.com/minikube/iso/minikube-v1.5.0.iso     --registry-mirror=https://registry.docker-cn.com --vm-driver=kvm2