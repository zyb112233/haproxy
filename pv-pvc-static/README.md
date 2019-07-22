1 部署nfs
yum install nfs-utils -y

＃配置
[root@nfs-140 ~]# cat /etc/exports
/k8s/data 192.168.122.0 (rw,sync)

#服务器启动
systemctl start nfs　　　　　　　　　\n
systemctl enable nfs
systemctl start rpcbind
systemctl enable rpcbind



#客户端
systemctl start rpcbind
systemctl enable rpcbind

#查看共享目录
showmout -e 192.168.122.140


２　在kubernetes部署
kubectl apply -f ./pv-pvc-static
