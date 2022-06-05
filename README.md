# kubernetes-101

<img src="https://www.pngkey.com/png/detail/246-2467736_the-leading-product-in-this-space-is-kubernetes.png">

## Installation:

#### Running a kubernetes Cluster:
There are several methods to spin up a kubernetes cluster in your local machine. You can run [**Minikube**](https://minikube.sigs.k8s.io/docs/start/) to start a single node kubernetes cluster in your own local machine.
The processes are simple. Here I am giving the steps for MAC. You will find steps for all os in their official documentation:
  #### MAC:
  - Install the minikube with **Homebrew** -  ```brew install minikube```
  - Start **Minikube** - ```minikube start```

#### We need one more thing to start working with kubernetes aka k8s:
  #### Kubectl:
  - Install with **Homebrew** - ```brew install kubectl```
  - Test if kubernetes cluster is running - ```kubectl get pod```
  - Output Should be ```No resources found in default namespace.```

What! That's all to run and test a kubernetes cluster in my computer?
Well, yes unfortunately that's all to run and test a kubernetes cluster

#### Let's make it more beautiful:
What I am doing is I am running a kubernetes cluster with minikube in my windows laptop. And accessing that cluster from my mac(I am lying. That's pathao's laptop :stuck_out_tongue_winking_eye:). It's like getting the feel of playing with a k8s cluster in cloud as a poor developer.
  #### Windows:
  - Let's open your windows/linux laptop
  - Install & start minikube on your windows machine. Assuming you have docker installed on your computer. If not, no worries. It's not rocket science to install docker.
  - Install kubectl tool.
  - Check if everything is alright by hitting this command ```kubectl get pod```
Noice! Now you are running a k8s cluster in your windows now we want to access that cluster from another computer in same network. Let's do that-
  #### Accessing remotely:
  - First we need to run proxy to expose minikube on local network. Run ```docker run chevdor/nginx-minikube-proxy:latest -p 18443:18443```. This will run a pod in docker. Next time make sure this pod is running to access the minikube from another machine.
  - Now let's copy 3 files from your windows machine to your mac. Go to your **C** partition. Then ```Users>{{your user}}>>.minikube```
      - client.crt (if you can't find go to profiles/minikube)
      - client.key (if you can't find go to profiles/minikube)
      - ca.crt
  #### Assuming you are on your mac now:
  - Now convert all the 3 files to their base64 version and note them on a text editor
  - If you don't know how to convert a file to base64. I am here.
      - ```cat filename```
      - ```echo "{{output from cat command}}" | grep base64```
  - Goto ```cd ~/.kube```
  - Backup the kube config by ```cp config config.backup```
  - Now we need to edit the cofig file. Open the config file in your favorite editor.
  - Add an item for ```clusters```
    ```yaml
    - cluster:
        certificate-authority-data: {{Put the base64 encoded ca.crt}}
        server: https://{{your windows machine's local network's ip address}}:18443
        name: minikube-remote
    ```
  - Add an item for ```contexts```
    ```yaml
    - context:
        cluster: minikube-remote
        user: minikube
      name: minikube-remote
    ```
 - Last one. Add a user under ```users```
    ```yaml
    - name: minikube
      user:
        client-certificate-data: {{Put the base64 encoded client.crt}}
        client-key-data: {{Put the base64 encoded client.key}}
    ```
 #### Let's test:
   - Run this command to switch the k8s context ```kubectl config use-context minikube-remote```
   - Now Run ```kubectl get pod``` and if you see expected output congrats! you are connected to a remote cluster.
