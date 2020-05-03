## Kubernetes的基本概念和术语

### master

Kubernetes里的Master指的是集群控制节点，在每个Kubernetes集群里都需要有一个Master来负责整个集群的管理和控制，基本上Kubernetes的所有控制命令都发给它，它负责具体的执行过程。Master通常会占据一个独立的服务器（多台做高可用），如果它宕机或者不可用，那么集群内容器应用的管理都会失效。

在Master上运行着这些关键的进程：

* Kubernetes API Server(Kube-apiserver)：提供了HTTP Rest接口的关键服务进程，是Kubernetes里所有资源的增、删、改、查等操作的唯一入口，也是集群控制的入口进程 。
* Kubernetes Controller Manager（kube-controller-manager）：Kubernetes里所有资源对象的自动化控制中心，可以将其理解为资源对象的总管。
* Kubernetes Scheduler（kube-scheduler）：负责资源调度（Pod调度）的进程，相当于数据都被保存在etcd（k8s集群使用etcd作为它的数据后端）中。

### node 

除了Master，Kubernetes集群中的其他机器被称为Node（Minion），可以是一台物理主机，也可以是一台虚拟机。Node是Kubernetes集群中的工作负载节点，每个Node都会被Master分配一些工作负载（Docker容器），当某个Node宕机时，其上的工作负载就会被Master自动转移到其他节点上去。

在每个Node上都运行着这些关键的进程：

* kubelet：负责Pod对应的容器的创建、启停等任务，同时和Master密切协作，实现集群管理的基本功能。
* Kube-proxy：实现Kubernetes Service的通信和负载均衡机制的重要组件。
* Docker-Engine(docker):Docker引擎，负责本机的容器创建和管理工作。

Node可以在运行期间动态增加到Kubernetes集群中，前提是在这个节点上已经正确安装、配置和启动了上述关键进程，在默认情况下kubelet会向Master注册自己，这也是Kubernetes推荐的Node管理方式。一旦Node被纳入集群管理范围，kubelet进程就会定时向Master汇报自身的情况，例如操作系统，Docker版本，机器的CPU和内存情况，以及当前有哪些Pod运行等，这样Master就可以获知每个Node的资源使用情况，并实现高效均衡的资源调度策略。而某个Node在超过指定时间不上报信息时，会被Master判定为“失联”，Node的状态被标记为不可用（Not Ready），随后Master会触发“工作负载大转移”的自动流程。