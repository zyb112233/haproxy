1 部署nfs
yum install nfs-utils -y

＃配置
[root@nfs-140 ~]# cat /etc/exports
/k8s/data 192.168.122.0 (rw,sync)

#服务器启动
systemctl start nfs
systemctl enable nfs
systemctl start rpcbind
systemctl enable rpcbind




#客户端
systemctl start rpcbind
systemctl enable rpcbind

#查看共享目录
showmout -e 192.168.122.140s

2　在kubernetes部署:
kubectl apply -f ./pv-pvc-static


3 查看结果
root@zyb-PC:/home/zyb/.local/share/Trash/files/pv-pvc# kubectl get pods
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-85456c8677-8qcfp   1/1     Running   0          57m
nginx-deployment-85456c8677-8xwdz   1/1     Running   0          57m
nginx-deployment-85456c8677-wjhgf   1/1     Running   0          57m

root@zyb-PC:/home/zyb/.local/share/Trash/files/pv-pvc# kubectl get pv,pvc
NAME                     CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM            STORAGECLASS   REASON   AGE
persistentvolume/my-pv   5Gi        RWX            Retain           Bound    default/my-pvc                           57m

NAME                           STATUS   VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
persistentvolumeclaim/my-pvc   Bound    my-pv    5Gi        RWX  
 
4 存在问题