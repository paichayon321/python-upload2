# python-upload2
This step below for Run test on katacoda at
https://www.katacoda.com/courses/kubernetes/launch-single-node-cluster

Copy script below on katacoda console for test

```
git clone https://github.com/paichayon321/python-upload2.git
cd python-upload2
docker pull python:3.9.5
docker run --privileged -p 30000:5000 --rm -e var1="value1" -it --volume "$(pwd):/app" python:3.9.5 bash -c "pip install flask && python /app/upload.py"
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
Run container in foregound mode  (-ti)
```
docker run --privileged -p 30000:5000 --rm -ti -e var1="value1 - file inside container" upload:1.0
```

Run container in foregound mode (-ti) and map external folder to container (-v)
```
docker run --privileged -p 30000:5000 --rm -ti -e var1="value1 - file on external container" --volume "$(pwd)/uploads:/app/uploads" upload:1.0
```

Run container in background mode (-d) and map external folder to container (-v)
```
docker run --privileged -p 30000:5000 --rm -d --name upload -e var1="value1 - file on external container and run background" --volume "$(pwd)/uploads:/app/uploads" upload:1.0
```

# Kubernetes - Deploy by yaml


# Kubernetes - Deploy by helm
