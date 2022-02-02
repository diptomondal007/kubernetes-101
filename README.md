# kubernetes-101

## Installation:

#### Running a kubernetes Cluster:
There are several methods to spin up a kubernetes cluster in your local machine. You can run [**Minikube**](https://minikube.sigs.k8s.io/docs/start/) to start a single node kubernetes cluster in your own local machine.
The processes are simple. Here I am giving the steps for MAC. You will find steps for all os in their official documentation:
  #### MAC
  - Install the minikube with **Homebrew** -  ```brew install minikube```
  - Start **Minikube** - ```minikube start```

#### We need one more thing to start working with kubernetes aka k8s:
  #### Kubectl
  - Install with ***Homebrew** - ```brew install kubectl```
  - Test if kubernetes cluster is running - ```kubectl get pod```
  - Output Should be ```No resources found in default namespace.```

What! That's all to run and test a kubernetes cluster in my computer?
Well, yes unfortunately that's all to run and test a kubernetes cluster

#### Let's make it more beautiful:
What I am doing is I am running a kubernetes cluster with minikube in my windows laptop. And accessing that cluster from my mac(I am lying. That's pathao's laptop :stuck_out_tongue_winking_eye:). It's like getting the feel of playing with a k8s cluster in cloud as a poor developer.
  #### Windows
  - Let's open your windows/linux laptop
  - Install & start minikube on your windows machine. Assuming you have docker installed on your computer. If not, no worries. It's not rocket science to install docker.
  - Install kubectl tool.
  - Check if everything is alright by hitting this command ```kubectl get pod```
