# assignment3

Build the image in Minikube's Docker daemon so the Helm deployments can use it
without pushing to a registry:

```bash
minikube start
eval $(minikube docker-env) # Linux/macOS
docker build -t darrenzwc-assignment3:latest .
```

On Windows PowerShell, use:

```powershell
minikube docker-env --shell powershell | Invoke-Expression
docker build -t darrenzwc-assignment3:latest .
```

Install two releases, each in its own namespace:

```bash
helm install greetings1 -n greetings1 --create-namespace ./greetings-chart \\
  --set nodePort=32764 \\
  --set greeting="This is greetings1" --set replicas=1
helm install greetings2 -n greetings2 --create-namespace ./greetings-chart \\
  --set nodePort=32765 \\
  --set greeting="This is greetings2" --set replicas=1
```

For Linux, set `URL1=http://$(minikube ip):32764` and
`URL2=http://$(minikube ip):32765`, then test (including
`curl $URL1/getk8sobjects` and `curl $URL2/getk8sobjects`). Delete releases
when finished with `helm delete greetings1 -n greetings1` and
`helm delete greetings2 -n greetings2`.
