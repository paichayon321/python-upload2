# python-upload2
This step below for Run test on katacoda at
https://www.katacoda.com/courses/kubernetes/launch-single-node-cluster

Copy script below on katacoda console for test

```
git clone https://github.com/paichayon321/python-upload2.git
cd python-upload2
docker pull python:3.9.5
docker run --privileged -p 30000:5000 --rm -e var1="value1" -it --volume "$(pwd):/app" python:3.9.5 bash -c "pip install flask && python /app/upload.py"

docker run --privileged -p 30000:5000 --rm -e var1="value1" -it --volume "$(pwd):/app" python:3.9.5 bash -c "pip install flask && pip install pyopenssl && openssl req -new -newkey rsa:4096 -days 3650 -nodes -x509 -subj '/C=TH/ST=TH/L=BKK/O=CTS/CN=mycert' -keyout key.pem -out cert.pem  && python /app/upload.py"
 
```
or after clone this project run initial script 
```
cd python-upload2
init-test-katacoda.sh
```

Click Katacoda Dashboard tab for test upload file

---

# Build Docker image
```
docker build -f ./deployment/docker/Dockerfile -t upload:1.0 .
```

# Run Docker Image
Run container in foregound mode (-ti) and pass environment variable value (-e var1="value1)
```
docker run --privileged -p 30000:5000 --rm -ti -e var1="value1 - file inside container" upload:1.0
```

Run container in foregound mode (-ti) and map external folder to container (--volume)
```
docker run --privileged -p 30000:5000 --rm -ti -e var1="value1 - file on external container" --volume "$(pwd)/uploads:/app/uploads" upload:1.0
```

Run container in background mode (-d) and map external folder to container (--volume)
```
docker run --privileged -p 30000:5000 --rm -d --name upload -e var1="value1 - file on external container and run background" --volume "$(pwd)/uploads:/app/uploads" upload:1.0
```
# Enable kubernetes and ingress on katacode
```
minikube start --wait=false
minikube addons enable ingress
```

# Kubernetes - Deploy by yaml
```
kubectl apply -f ./deployment/k8s
```


# Kubernetes - Deploy by helm

# Ingress
https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/

# Insall helm3
```
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
mv /usr/bin/helm /usr/bin/helm2
cp /usr/local/bin/helm /usr/bin/helm
helm version
```

# Create helm chart
```
helm create ./deployment/helm/upload
```
# Modify Chart
```
vi ./deployment/helm/upload/values.yaml


```


# Run Helm chart
```
helm upgrade upload --dry-run --debug ./deployment/helm/upload --install
helm upgrade upload ./deployment/helm/upload --install

```

# TLS ingress
```
openssl req -new -newkey rsa:4096 -days 3650 -nodes -x509 -subj '/C=TH/ST=TH/L=BKK/O=CTS/CN=mycert' -keyout key.pem -out cert.pem
kubectl create secret tls upload-tls --key key.pem --cert cert.pem

```
