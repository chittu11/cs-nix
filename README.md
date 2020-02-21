
Instructions:
1. This will be used for one master and many worker nodes on-prem kubernetes setup.
2. Needs to setup password less authentication(trust) between kube master node to worker nodes in order to work Ansible deployment script to work
3. There is a file "hosts" available in "centos" directory, Just make your entries of your all kubernetes nodes. this is local ansible inventory file
4. Provide your server details in "env_variables" available in "centos" directory.
5. Deploy the ssh key from master node to other nodes for password less authentication.

   ssh-keygen
   
   Copy the public key to all nodes including your master node and make sure you are able to login into any nodes without password.
   sshpass -f abc ssh-copy-id <hostname> or run it in loop
   
6. Run "settingup_kubernetes_cluster.yml" playbook to setup all nodes with master and worker node config.

   ansible-playbook settingup_kubernetes_cluster.yml
   

7. Verify the configuration from master node.

      kubectl get nodes

What are the files this repository has?:

ansible.cfg - Ansible configuration file created locally.

hosts - Ansible Inventory File

env_variables - Main environment variable file where we have to specify based on our environment.

settingup_kubernetes_cluster.yml - Ansible Playbook to perform prerequisites ready, setting up nodes, configure master node, and joining workers nodes to master node.

configure_worker_nodes.yml - Ansible Playbook to join worker nodes with master node.

clear_k8s_setup.yml - Ansible Playbook helps to delete entire configurations from all nodes.
before running this playbook, please run the below commands on all nodes to wipe out kubernetes cluster 
#kubeadm reset <press y>
#rm -rf $HOME/.kube/config

