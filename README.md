# python-upload2
Run test on katacoda
https://www.katacoda.com/courses/kubernetes/launch-single-node-cluster

git clone https://github.com/paichayon321/python-upload2.git
cd python-upload2
docker pull python:3.9.5
docker run --privileged -p 30000:5000 --rm -it --volume "$(pwd):/app" python:3.9.5 bash -c "pip install flask && python /app/upload.py"

