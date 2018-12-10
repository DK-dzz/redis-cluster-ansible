# redis-cluster-ansible
deploy redis cluster by ansible

#step 1 </br>
[root@ansible-01-sz ~]# vim  redisnodes </br>
[redisnodes] </br>
192.168.1.3 </br>
192.168.1.4 </br>
192.168.1.5 </br>
192.168.1.6 </br>
192.168.1.7 </br>
192.168.1.8 </br>

#step 2 </br>
[root@ansible-01-sz ~]#vim redis-cluster-ansible.yaml </br>
... </br>
  vars: </br>
    - redis_port: ['6379','6380','6381']  ## add ports ,like  ['6379','6380','6381','6382','more']  </br>
    - redis_home: '/app/redis'  ## set storage path of conf、data、log  </br>
    - redis_version: 'redis-4.0.11' ## set redis verion  </br>
    - redis_url: "http://download.redis.io/releases/{{ redis_version }}.tar.gz" </br>
    - IP: "{{ ansible_ens33['ipv4']['address'] }}" ## set os interface like :  ansible_eth0['ipv4']['address'] </br>
... </br>


#step 3 </br>
[root@ansible-01-sz ~]# ansible-playbook -i redisnodes  redis-cluster-ansible.yaml </br>



#notice : create cluster by yourself </br>
[root@ansible-01-sz ~]# redis-trib.rb create --replicas 1 IP1:PORT1 IP2:PORT2 IP3:PORT4 ... <<EOF </br>
yes </br>
 </br>
EOF </br>
