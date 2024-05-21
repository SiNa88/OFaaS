# OFaaS
Setting up an OpenFaaS project

## Helps
To set up the project, I referred to the following URLs:

https://go.dev/doc/install

https://github.com/kubernetes-sigs/kind

https://slopezza.medium.com/openfaas-installation-and-first-python-function-part-i-fa429053e8df

https://docs.openfaas.com/deployment/kubernetes/

https://devpress.csdn.net/k8s/62eb8a4b20df032da732b69f.html

https://blog.alexellis.io/first-faas-python-function/

https://blog.alexellis.io/troubleshooting-on-kubernetes/

https://stackoverflow.com/questions/52369247/namespace-stuck-as-terminating-how-i-removed-it

https://chaoscodes.github.io/2019/06/11/My-first-try-in-OpenFass/

https://www.freshbrewed.science/kubernetes-serverless-openfaas/index.html

https://github.com/s8sg/faas-flow/issues/119

https://stackoverflow.com/questions/40686151/kubernetes-pod-gets-recreated-when-deleted

https://chaoscodes.github.io/2019/06/11/My-first-try-in-OpenFass/

## Installation

Then, I used the following commands to install the OFaaS on Ubuntu 20.04, running Kubernetes 1.21:

  ```curl -SLsf https://get.arkade.dev/ | sudo sh```
  
  ```sudo arkade install openfaas```

  ```curl -sSL https://cli.openfaas.com | sudo sh```

  ```kubectl get ns openfaas-fn -o json |   jq '.spec.finalizers=[]' |   curl -X PUT http://localhost:8001/api/v1/namespaces/openfaas-fn/finalize -H "Content-Type: application/json" --data @-```
  
  ```kubectl apply -f https://raw.githubusercontent.com/openfaas/faas-netes/master/namespaces.yml```
  
  ```wget https://go.dev/dl/go1.20.2.linux-amd64.tar.gz```
  
  ```rm -rf /usr/local/go```
  
  ```sudo tar -C /usr/local -xzf go1.20.2.linux-amd64.tar.gz```
  
  ```export PATH=$PATH:/usr/local/go/bin```
  
  ```go version```
  
  ```docker stop kind-registry && docker rm kind-registry```
  
  ```kubectl config current-context```
  
  ```curl -Lo ./kind "https://kind.sigs.k8s.io/dl/v0.18.0/kind-$(uname)-amd64"```
  
  ```chmod +x ./kind```
  
  ```sudo mv ./kind /usr/local/bin/kind```
  
  ```which kind```
  
  ```nano kind-with-registry.sh```
  
  ```sudo chmod +x kind-with-registry.sh```
  
  ```./kind-with-registry.sh```
  
  ```kubectl config current-context```
  
  ```kubectl cluster-info```
  
  ```docker logs -f kind-registry```
  
  ```docker ps -a```
  
  ```sudo arkade install openfaas```
  
  ```kubectl get pods -n openfaas```
  
  ```faas-cli template store list```

### Port forwarding to have function invocation
  ```kubectl port-forward -n openfaas svc/gateway 8080:8080```

  ```PASSWORD=$(kubectl get secret -n openfaas basic-auth -o jsonpath="{.data.basic-auth-password}" | base64 --decode; echo)```
  
  ```env | grep PASSWORD```
  
  ```echo -n $PASSWORD | faas-cli login --username admin --password-stdin```
  
  ```echo -n $PASSWORD```
  
  ```faas-cli list```
  
  ```faas-cli template store list```
  
  ```nano hello-python/handler.py```
  
  ```nano hello-python.yml```
  
  ```faas-cli build -f ./hello-python.yml```
  
  ```faas-cli registry-login --username sina88 --password-stdin```
  
  ```faas-cli deploy -f ./hello-python.yml```
  
  ```curl http://127.0.0.1:8080/function/hello-python -d  "it's name here"```
  
  ```kubectl get pods -n openfaas```
  
  ```docker images | grep hello-python```
  
  ```kubectl get pods --all-namespaces```
  
  ```kubectl delete replicasets.apps  -n openfaas-fn  hello-python2-5799749f57```
  
  ```kubectl delete pods -n openfaas-fn hello-python2-5799749f57-pnwq4 --force```
  
  ```kubectl delete replicasets.apps  -n openfaas-fn  hello-python-598c869b9d```
  
  ```kubectl delete pods -n openfaas-fn hello-python-598c869b9d-mt2f8 --force```
  
  ```kubectl get events --sort-by=.metadata.creationTimestamp -n openfaas-fn --watch```


## An example

[Step-1: commands](https://github.com/SiNa88/sina88.github.io/blob/main/openfaas/Step_0_0.jpg) and [Step-2: GUI](https://github.com/SiNa88/sina88.github.io/blob/main/openfaas/Step_0_1.jpg)



   
