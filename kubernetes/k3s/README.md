### K3S Installation:

##### Run on the VERY FIRST Master Node (192.168.50.240)
```bash
curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" sh -s - server \
--token=SUPERSECRETTOKEN \
--tls-san subdomain.yourdomain.com --tls-san 192.168.x.x \
--cluster-init
```

##### Run on the next Master Nodes (192.168.50.241, 192.168.50.242)
```bash
curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" sh -s - server \
--token=SUPERSECRETTOKEN \
--tls-san subdomain.yourdomain.com --tls-san 192.168.x.x \
--server https://192.168.x.x:6443
```

##### Run on the Worker Nodes (192.168.50.241)
```bash
curl -sfL https://get.k3s.io | K3S_URL=https://192.168.x.x:6443 K3S_TOKEN=SUPERSECRETTOKEN sh -
```

