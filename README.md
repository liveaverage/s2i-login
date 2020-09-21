# s2i-login

### Testing

Once the container is built and the route has been weighted you can test:
```
while true; do curl -s https://login.apps.go.z.shifti.us/ | grep 'v[1-3]' | awk '{print($8)}' ; done
```
