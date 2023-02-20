# Linux-Practice

## Present Working Directory
```
pwd
```

## Change Directory
```
cd /home
```

## Listing Hidden Files
```
ls -a
```

## Creating & Viewing Files
### View File
```
cat filename
```
### Create File
```
cat > filename
```
### The syntax to combine 2 files
```
cat file1 file2 > newfilename
```

## Deleting Files
```
rm filename
```

## Moving and Re-naming files
```
mv filename new_file_location
```

## Directory Manipulations
### Creating Directories
```
mkdir directoryname
```
### Removing Directories
```
rmdir mydirectory
```

## Installing Software
```
sudo apt-get update
```

## Linux Mail Command
```
sudo apt-get install mailutils
mail -s 'subject' -c 'cc-address' -b 'bcc-address' 'to-address'
```

# Kubernetes Cluster Create

## connect to terminal
```
ssh root@[ip]
```
## Get sudo working
```
sudo -l
```
## install curl and apt-transport-https
```
sudo apt-get update && sudo apt-get install -y apt-transport-https curl
```
## add key to verify releases
```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```
## add kubernetes apt repo
```
cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
```
## install kubelet, kubeadm and kubectl
```
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
```
## install docker
```
sudo apt-get install docker.io
```
## apt-mark hold is used so that these packages will not be updated/removed automatically
```
sudo apt-mark hold kubelet kubeadm kubectl
```
## master node configeration

### get pod token to connect each nodes
```
export MASTER_IP=<IP-of-Node>
kubeadm init --apiserver-advertise-address=${MASTER_IP} --pod-network-cidr=10.244.0.0/16
```

## The connection to the server localhost:8080 was refused - did you specify the right host or port?
### then we can do follow command
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```


## add nginx 
```
kubectl create deployment nginx --image nginx
kubectl expose deployment nginx --type NodePort --port 80
```

## then we can see nginx using follow cmd
```
kubectl get all
```
## use nodeport and master ip
## kubernetes dashboard setup

### see whether nodes working
```
kubectl get nodes
```

### apply UI
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.6.1/aio/deploy/recommended.yaml
```

### dashboard status
```
kubectl get pods -n kubernetes-dashboard
```

### change nodeport
```
kubectl -n kubernetes-dashboard edit svc kubernetes-dashboard
```

### get token
```
kubeadm token create --print-join-command
```

### exit and save power shel
```
need to enter using "i"
esc -> :wq! -> enter
```

### how to exit
```
watch kubectl get pods --all-namespaces
kubectl proxy
```









