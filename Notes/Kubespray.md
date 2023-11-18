
Deploy kubernetes with Kubespray. Here, I define steps :
do step 1 and 2 in master node.
1. Setup ssh keys
	1. ssh-keygen
	2. ssh-copy-id `username@ip`
	3. sudo apt-get install keychain
	4. add following two lines to end of  `.bashrc` in your home directory.
	```
	keychain id_rsa . ~/.keychain/`uname -n` -sh
	```

2. Install kubespray 
	1. `sudo apt-get install git`
	2. `sudo apt-get install python-pip3`
	3. `git clone https://github.com/kubernetes-sigs/kubespray.git`
	4. `sudo pip3 install -r kubespray/requirements.txt` 
	5. In default mode we don't have log file, then you need to define log directory. 
	```
	vim ansible.cfg
	```
	 Add the below line in that directory.
	 ```
	 log = ./kubespray.log
	 ```
	 6. Now we need to define our hots in inventory file
	 ```
	 cp -r kubespray/inventory/sample kubespary/inventory/{deployment name}
	```
	7. Now define our host just be passion in this document I use hostname so you need to define hosts and IP in `/etc/host`. The inventory file it should be like this:
	```
	[all]
	masternode1
	worckernode1
	workernode2
	workernode3
	
	[kube_control_plane]
	masternode1
	
	[kube_node] 
 	worckernode1
	workernode2
	workernode3

	[calico_rr]

    [k8s_cluster:children]
    kube_control_plane
    kube_node
    calico_rr
    ```

	 8. In kubespray default CNI is calico if you want to change this follow this steps: 
		 1. Open `inventory/{deployment name}/group_vars/k8s-cluster/k8s-cluster.ym`
		```
		kube_network_plugin: flannel
		```
	9. Now install kubespray dependencies, we can see that in `requirements.txt`  
	```
	pip3 install -r requirements.txt
    ```
	10.  Add ansible to `/usr/local/bin`
	11. Now you can run your pay book.
	```
	ansible-playbook -i {inventory.ini path like inventory/cluster/inventory.inu} --become --become-user=root -k {cluster.yaml}
   ```