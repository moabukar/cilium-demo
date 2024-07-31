# Cilium demo

- Lab/demo to play with Cilium (CNI for K8s)
- And to get bettet with K8s networking.


- Create an ubuntu and ssh into it

```bash

curl https://raw.githubusercontent.com/moabukar/cilium-demo/main/k8s-no-cni.sh | sh

kubectl get nodes
```

## Install cilium

```bash

wget https://github.com/cilium/cilium-cli/releases/latest/download/cilium-linux-amd64.tar.gz
sudo tar xzvfC cilium-linux-amd64.tar.gz /usr/local/bin
cilium version

## install cilium cni
cilium install
cilium status
kubectl get nodes

kubectl get pod -A

```

## Network testing

```bash

curl http://169.254.169.254/latest/meta-data/public-ipv4
curl -s checkip.dyndns.org | sed -e 's/.*Current IP Address: //' -e 's/<.*$//'


ip address | head

```

## Pod networking

```bash

kubectl run web --image=httpd
kubectl get pod -o wide

## Check the Cilium IP Address Manager (IPAM) configuration:
cilium config view | grep cluster-pool

## check tunnel type:
cilium config view | grep tunnel


## Test pod net

kubectl run client -it --image=busybox
ip a
ping -c 3 <WEB POD IP>
wget -qO - <WEB POD IP>

## clean up
exit
kubectl delete pod client web


```


## Services

