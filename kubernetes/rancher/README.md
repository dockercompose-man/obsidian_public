### Rancher Install (Docker)
https://phoenixnap.com/kb/install-rancher-on-ubuntu

```
sudo docker run -d --restart=unless-stopped -p 8080:8080 rancher/server:stable
```

##### get the certificate from the cluster
```bash
echo | openssl s_client -showcerts -connect 192.168.50.240:6443 2>/dev/null | openssl x509 -outform PEM
```

##### 1.  Copy the output of the above command (the certificate) and save it to a file, for example, `kube.crt`.
##### 2. Configure your CLI tool, such as `kubectl`, to use the certificate file:
```bash
kubectl config set-cluster k3s-orangefarm --server=https://192.168.50.240:6443 --certificate-authority=/root/.vault/kube.crt
```

```bash
kubectl config set-cluster k3s-orangefarm --server=https://192.168.50.240:6443 --certificate-authority=/root/.vault/kube.crt
```
