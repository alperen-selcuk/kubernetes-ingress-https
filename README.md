# kubernetes-ingress-https

öncelikle web sitemiz için bir lets encrypt sertifika yaratacağız.

```
apt install certbot -y

sudo certbot certonly --manual --preferred-challenges=dns --email alperenhasanselcuk@gmail.com  --server https://acme-v02.api.letsencrypt.org/directory --agree-tos -d myweb.dev-ops.expert

```

daha sonra kubernetes e bu sertifika ve key i eklemek için secret kullanacağız.

```
kubectl create secret tls test-tls --key=key --cert=crt
```

sonra da ingress controller kuracağız.

```
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

helm repo update

helm install ingress-nginx ingress-nginx/ingress-nginx -n ingress-nginx --create-namespace
````

denemek için bir nginx app deploy edelim.

```
kubectl create deploy myweb --image=nginx replicas=2

kubectl expose deploy/myweb --port 80
```
