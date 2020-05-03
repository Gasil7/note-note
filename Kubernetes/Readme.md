### Kubernetes的基本概念和术语

> master

Kubernetes里的Master指的是集群控制节点，在每个Kubernetes集群里都需要有一个Master来负责整个集群的管理和控制，基本上Kubernetes的所有控制命令都发给它，它负责具体的执行过程。Master通常会占据一个独立的服务器（多台做高可用），如果它宕机或者不可用，那么集群内容器应用的管理都会失效。

在Master上运行着这些关键的进程：

* Kubernetes API Server(Kube-apiserver)：提供了HTTP Rest接口的关键服务进程，是Kubernetes里所有资源的增、删、改、查等操作的唯一入口，也是集群控制的入口进程 。
* Kubernetes Controller Manager（kube-controller-manager）：Kubernetes里所有资源对象的自动化控制中心，可以将其理解为资源对象的总管。
* Kubernetes Scheduler（kube-scheduler）：负责资源调度（Pod调度）的进程，相当于数据都被保存在etcd（k8s集群使用etcd作为它的数据后端）中。

>node