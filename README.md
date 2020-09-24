# s2i-login

### Configuration

```

oc new-app --docker-image=quay.io/shifti/login-ui:v1 --name=login-v1
oc expose svc/login-v1

oc new-app --docker-image=quay.io/shifti/login-ui:v2 --name=login-v2
oc expose svc/login-v2

oc new-app --docker-image=quay.io/shifti/login-ui:v3 --name=login-v3
oc expose svc/login-v3
 
oc expose svc/login-v2 --hostname=login.apps.${TF_VAR_cluster_name}.${TF_VAR_cluster_basedomain} --name=login
oc set route-backends login login-v1=50 login-v2=50
 ```

### Testing

Once the container is built and the route has been weighted you can test:
```
while true; do curl -s https://login.apps.go.z.shifti.us/ | grep 'v[1-3]' | awk '{print($8)}' ; done
```
