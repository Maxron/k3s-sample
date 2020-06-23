# K3S Setup tutorial

----

## Setup step:
1. Setup server node
2. Setup agent node


### Setup server node

```bash
$ curl -sfL https://get.k3s.io | sh -
```
Check for Ready node, takes maybe 30 seconds.  

```bash
$ k3s kubectl get node
```

Then, get token from server node, this will used by agent node.  
```bash
$ sudo cat /var/lib/rancher/k3s/server/node-token
```

### Setup agent node

1. Add k3s server ip to _/etc/hosts_ file.  
```bash
$ sudo su 
$ echo "192.168.55.130 k3s-m" >> /etc/hosts
$ exit
```  

2. Install agent, this will used the token which get from previous step.  
```bash
$ curl -sfL https://get.k3s.io |K3S_URL=https://k3s-m:6443 K3S_TOKEN=XXXXXXXXXX sh -
```  

3. After installed, check the state on server node.  
```bash
$ sudo k3s kubectl get nodes
NAME     STATUS   ROLES    AGE    VERSION
k3s-m    Ready    master   164m   v1.18.4+k3s1
k3s-s1   Ready    <none>   17m    v1.18.4+k3s1
```

### uninstall 
- Server node: `k3s-killall.sh`
- Agent node: `k3s-agent-uninstall.sh`

## Reference:
- [K3S github](https://github.com/rancher/k3s/blob/master/README.md)
- [K3sup](https://github.com/alexellis/k3sup)
