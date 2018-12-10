# redis-cluster-ansible
deploy redis cluster by ansible


#step 1: edit ip for redis nodes </br>
[root@ansible-01-sz ~]# vim  redisnodes </br>
[redisnodes] </br>
192.168.1.3 </br>
192.168.1.4 </br>
192.168.1.5 </br>
192.168.1.6 </br>
192.168.1.7 </br>
192.168.1.8 </br>
......


#step 2:edit yaml </br>
[root@ansible-01-sz ~]#vim redis-cluster-ansible.yaml </br>
... </br>
  vars: </br>
    - redis_port: ['6379','6380','6381']  ## add ports ,like  ['6379','6380','6381','6382','more']  </br>
    - redis_home: '/app/redis'  ## set storage path of conf、data、log  </br>
    - redis_version: 'redis-4.0.11' ## set redis verion  </br>
    - redis_url: "http://download.redis.io/releases/{{ redis_version }}.tar.gz" </br>
    - IP: "{{ ansible_ens33['ipv4']['address'] }}" ## set os interface like :  ansible_eth0['ipv4']['address'] </br>
... </br>


#step 3: install</br>
[root@ansible-01-sz ~]# ansible-playbook -i redisnodes  redis-cluster-ansible.yaml </br>




#notice : create cluster by yourself </br>
[root@ansible-01-sz ~]# redis-trib.rb create --replicas 1 IP1:PORT1 IP2:PORT2 IP3:PORT4 ... <<EOF </br>
yes </br>
 </br>
EOF </br>


#notice : tree of file
tree /app/redis/</br>
[root@ansible-01-sz ~]# /app/redis/</br>
├── 6379</br>
│?? ├── conf</br>
│?? │?? └── redis-6379.conf</br>
│?? ├── data</br>
│?? │?? ├── dump.rdb</br>
│?? │?? └── nodes.conf</br>
│?? └── logs</br>
│??     └── redis-6379.log</br>
├── 6380</br>
│?? ├── conf</br>
│?? │?? └── redis-6380.conf</br>
│?? ├── data</br>
│?? │?? ├── dump.rdb</br>
│?? │?? └── nodes.conf</br>
│?? └── logs</br>
│??     ├── redis-6380.log</br>
│??     └── redis-6380.pid</br>
├── 6381</br>
│?? ├── conf</br>
│?? │?? └── redis-6381.conf</br>
│?? ├── data</br>
│?? │?? ├── dump.rdb</br>
│?? │?? └── nodes.conf</br>
│?? └── logs</br>
│??     ├── redis-6381.log</br>
│??     └── redis-6381.pid</br>
├── 6382</br>
│?? ├── conf</br>
│?? │?? └── redis-6382.conf</br>
│?? ├── data</br>
│?? │?? ├── dump.rdb</br>
│?? │?? └── nodes.conf</br>
│?? └── logs</br>
│??     ├── redis-6382.log</br>
│??     └── redis-6382.pid</br>
├── 6383</br>
│?? ├── conf</br>
│?? │?? └── redis-6383.conf</br>
│?? ├── data</br>
│?? │?? ├── dump.rdb</br>
│?? │?? └── nodes.conf</br>
│?? └── logs</br>
│??     ├── redis-6383.log</br>
│??     └── redis-6383.pid</br>
└── 6384</br>
    ├── conf</br>
    │?? └── redis-6384.conf</br>
    ├── data</br>
    │?? ├── dump.rdb</br>
    │?? └── nodes.conf</br>
    └── logs</br>
        ├── redis-6384.log</br>
        └── redis-6384.pid</br>
</br>




[root@ansible-01-sz ~]# find  /etc/init.d/  -name redis*</br>
/etc/init.d/redis_6382</br>
/etc/init.d/redis_6383</br>
/etc/init.d/redis_6380</br>
/etc/init.d/redis_6381</br>
/etc/init.d/redis_6384</br>
/etc/init.d/redis_6379</br>
