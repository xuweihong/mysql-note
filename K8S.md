# pod

- 最小的部署及管理单位，位置管理，拷贝复制，资源共享，依赖关系都是自动处理的。

- 进程被发送TERM信号，优雅退出时间是30s，一旦优雅退出期限过了，kill信号会发送到进程，pod会从api服务器中删除。



# node 

- 每个Node节点上至少要运行container runtime（比如docker或者rkt）、kubelet和kube-proxy服务。

- Taints和tolerations用于保证Pod不被调度到不合适的Node上，Taint应用于Node上，而toleration则应用于Pod上

# Replication Controller

- Replication Controller只会对那些 RestartPolicy = Always的 Pod 的生效，（RestartPolicy的默认值就是Always）

- RC 控制着 pod 的生命周期，通过模板来生成 pod，通过修改值来伸缩 pod 的数量。

# ReplicaSet

- 虽然 ReplicaSets 可以独立使用，但是今天它主要被 Deployments 作为协调 pod 创建，删除和更新的机制。

- ReplicaSet 和 RC 的唯一区别是现在的选择器支持，RC只支持基于等式的 selector,而 ReplicaSet 还支持新的，基于集合的 selector（version in (v1.0, v2.0)或env notin (dev, qa)）。

# Service

- 一个 Kubernete 服务是一个最小的对象，类似 pod,和其它的终端对象一样,我们可以朝 api server 发送请求来创建一个新的实例

- Kubernetes 支持两种方式的来发现服务 ，环境变量和 DNS

- 调用外部服务

    - ClusterIP:使用一个集群固定IP，这个是默认选项
    
    - NodePort：使用一个集群固定IP，但是额外在每个POD上均暴露这个服务，端口
    
    - LoadBalancer：使用集群固定IP，和NODE Port,额外还会申请申请一个负载均衡器来转发到服务（load balancer ）
    
# Deployment

- 典型的应用场景包括：
  
  - 定义 Deployment 来创建 Pod 和 ReplicaSet
  - 滚动升级和回滚应用
  - 扩容和缩容
  - 暂停和继续 Deployment
  
