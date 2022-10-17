---
layout: post
categories: kubernetes
---
## 동기
프로그래밍적으로 쿠버네티스 클러스터 내의 리소스의 annotation을 동적으로 변경해줘야할 필요가 있어서 방법을 찾던 중, REST API를 이용해 클러스터를 제어하는 방법을 찾게 됨. ([access-cluster-api](https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/))


## 목적
kubectl을 이용한 명령어를 동작시킬 때, 실제로 어떤 형태로 클러스터에 전송이 되는지 확인한다.


## 방법
먼저 kubectl을 이용해 namespace 목록을 가져오는 명령어는 아래와 같이 심플하다. 그리고 현재 클러스터의 namespace 목록이 출력된다.
```
kubectl get ns

NAME               STATUS   AGE
default            Active   4d5h
kube-node-lease    Active   4d5h
kube-public        Active   4d5h
kube-system        Active   4d5h
```



이때 뒤에 옵션을 추가해주면, 어떤 url로 어떤 요청을 보내는지 출력이 된다. 값은 1부터 올려가며 확인할 수 있는데, 점점 자세해진다. 개인적으론 8이 request, response 확인하기에 적절한거 같다. (자세한 설명은 [kubectl-output-verbosity-and-debugging](https://kubernetes.io/docs/reference/kubectl/_print/#kubectl-output-verbosity-and-debugging)를 참고)
```
kubectl get ns --v 6
I1017 16:15:48.367777   40015 loader.go:374] Config loaded from file:  /path/to/.kube/config
I1017 16:15:48.983946   40015 round_trippers.go:553] GET https://api-server-url/api/v1/namespaces?limit=500 200 OK in 613 milliseconds
NAME               STATUS   AGE
default            Active   4d5h
kube-node-lease    Active   4d5h
kube-public        Active   4d5h
kube-system        Active   4d5h
```
