 ## NFS-SERVER:

1. Install the package on the server. 
	- `sudo apt install nfs-kernel-server nfs-common portmap` 
	- `sudo systemctl start nfs-server`
	-  `sudo mkdir -p /srv/nfs/kubedat`
	- `sudo chown -R nobody: /srv/nfs/kubedat`
	- `vim /etc/exports` And add the below line : `/srv/nfs/kubedat *(rw,sync,no_subtree_check,no_root_squash,insecure)` 
	- `sudo chmod -R 777 /srv/nfs/`
	- `sudo vim /etc/exports`  Add `/srv/nfs/kubedat *(rw,sync,no_subtree_check,no_root_squash,insecure)`
	- `sudo exportfs -rav`
	- `showmount -e`

## On-Worker-node
you need to do this for each server you have:
2. Connect worker to nfs-server
	- `showmount ip `
	-  `sudo mount -t nfs 10.227.222.154:/srv/nfs/kubedat /mnt`
	-  `mount | grep kubedat`

## On-Master-node
3. clone the nfs-subdir-external and got to the deployment directory.
	- `git clone https://github.com/kubernetes-sigs/nfs-subdir-external-provisioner.git`
	- Deploy `rbac`, `class` and `deploy`
	- you need this image to all worker node: `registry.k8s.io/sig-storage/nfs-subdir-external-provisioner:v4.0.2`
 If you have problem with create app like redis, but you will see error can't mount install nfs with helm:
 ```
 $ helm repo add nfs-subdir-external-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner/
$ helm install nfs-subdir-external-provisioner nfs-subdir-external-provisioner/nfs-subdir-external-provisioner 
    --set nfs.server=x.x.x.x \
    --set nfs.path=/exported/path
```


sum(rate(container_cpu_usage_seconds_total{namespace="$namespace", pod="$pod", image!="", cluster="$cluster"}[$__rate_interval])) / sum(kube_pod_container_resource_limits{namespace="$namespace", pod="$pod", resource="cpu", job=~"$job", cluster="$cluster"})