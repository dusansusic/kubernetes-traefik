# kubernetes-traefik
Traefik has this feature in versions 1.7 and newer

## How to deploy Traefik Ingress Controller to K8S

- Create namespace:
```
kubectl create namespace traefik
```

- Create TLS certificate:
```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ./tls.key -out ./tls.crt -subj "/CN=*.example.com"
```

- Create a TLS secret:
```
kubectl create secret tls -n traefik traefik-ui-tls-cert --key ./tls.key --cert ./tls.crt
```

- Modify `entryPoints.traefik.auth.basic` section of `deployment.yaml` with new admin username/password
```
htpasswd -nb admin new_password_you_choose
```

- Apply deployment file:
```
kubectl apply -f deployment.yaml
```
