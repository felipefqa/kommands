# kommands
kubernetes common commands without so much typing

![](kommands.svg)

## install

`git clone https://github.com/javimox/kommands ~/.kube/kommands/`

**bash**  
> `echo "source ~/.kube/kommands/.kommands" >> ~/.bashrc && source ~/.bashrc`

**zsh**  
 > `echo "source ~/.kube/kommands/.kommands" >> ~/.zshrc && source ~/.zshrc`

## usage

All the commands below accept as parameter a number or a name. Autocomplete is enabled for names.

**k**ommands **g**et and their `kubectl` equivalents
<pre>
kgpo  ->  kubectl get pods
kgpvc ->  kubectl get pvc
kgsvc ->  kubectl get svc
</pre>

**k**ommands **d**el:
<pre>
kdpo  -> kubectl delete pod
kdpvc -> kubectl delete pvc
kdsvc -> kubectl delete svc
</pre>

**k**ommand **desc**ribe:
<pre>
kdesc -> kubectl describe
</pre>

**k**ommand **s**how **co**ntainers:  
`ksco`  : it returns the name of the containers that run in a specific pod

**k**ommand **e**xecute `sh`:  
`kesh`  : it opens a shell in a specific pod/container

## examples

#### get pods and their number
```
$ kgpo 
 0 NAME                 READY   STATUS             RESTARTS   AGE
 1 echo-pod-pvc         0/1     Pending            0          103m
 2 first-pod            1/1     Running            0          2d6h
 3 pod-two-containers   2/2     Running            0          83m
```

#### get pod number 3
```
$ kgpo 3
 0 NAME                 READY   STATUS             RESTARTS   AGE
 3 pod-two-containers   2/2     Running            0          84m
```

#### show containers of the pod number 3
```
$ ksco 3
 0 NAME
 1 i-am-the-first-container-in-this-pod
 2 i-am-then-the-second-container
```

#### open a shell in a container of a pod using names
```
$ kesh pod-[TAB] [TAB]
i-am-the-first-container-in-this-pod  i-am-then-the-second-container

$ kesh pod-two-containers i-am-then-the-second-container
You are now in pod: pod-two-containers -c i-am-then-the-second-container
/ # 
```

#### open a shell in a container of a pod using numbers
pod number 3 , container number 2
```
$ kesh 3 2
You are now in pod: pod-two-containers -c i-am-then-the-second-container
/ # 
```

#### get persistent volume claims
```
$ kgpvc
 0 NAME          STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS       AGE
 1 echo-cache2   Bound    pvc-49704fde-7d19-446c-b9f2-192e297e7f0a   1Gi        RWO            do-block-storage   111m
 2 pvc-1         Bound    pvc-4e902e87-0df7-4c3c-827c-a8c7cfd75fa5   1Gi        RWO            do-block-storage   93m
```

#### delete persistent volume claim using its number
```
$ kdpvc 2
do you want to remove pvc-1 (y/N)? y
persistentvolumeclaim "pvc-1" deleted
```

#### get services
```
$ kgsvc
 0 NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
 1 echo-web-svc-nodeport   NodePort    10.245.124.76    <none>        8080:31777/TCP   112m
 2 kubernetes              ClusterIP   10.245.0.1       <none>        443/TCP          2d6h
 3 test-app                ClusterIP   10.245.109.229   <none>        8080/TCP         113m
 ```
 
#### describe service number 3
```
$ kdesc svc 3
Name:              test-app
Namespace:         default
Labels:            name=test-app
Annotations:       Selector:  app=echo-app
Type:              ClusterIP
IP:                10.245.109.229
Port:              echo  8080/TCP
TargetPort:        8080/TCP
Endpoints:         <none>
Session Affinity:  None
Events:            <none>
```

## license

The source code is licensed under the [GNU General Public License v3.0][GPLv3].

Copyright (C) 2020 jmox(at)pm.me

This program is free software: you can redistribute it and/or modify it under
the terms of the GNU General Public License as published by the Free Software
Foundation, either version 3 of the License, or (at your option) any later
version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with
this program.  If not, see <http://www.gnu.org/licenses/>.

[GPLv3]: https://www.gnu.org/licenses/gpl-3.0.txt
[kommands]: https://github.com/javimox/kommands
