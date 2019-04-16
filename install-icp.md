---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# Installation checklist
{: #inst-install-icp}

Learn how to install the {{site.data.keyword.aios_short}} tool into {{site.data.keyword.icpfull}} for Data.
{: shortdesc}

The {{site.data.keyword.icpfull_notm}} environment is a Kubernetes-based container platform that can help you quickly modernize and automate workloads that are associated with the applications and services you use. You can develop and deploy on your own infrastructure and in your data center which helps to mitigate risk and minimize vulnerabilities.

## Hardware requirements
{: #inst-hw}

Always refer to [System requirements for {{site.data.keyword.icpfull_notm}} for Data ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_1.1.0/com.ibm.icpdata.doc/zen/install/reqs-ent.html){: new_window} for the most current requirements.

### Operating system requirements
{: #inst-hwo}

| Operating system | Minimum level | Hardware | Bitness
|:---|:---:|:---:|:---:
|Red Hat Enterprise Linux (RHEL) Server 7 | 7.5 | x86-64 | 64-Exploit ||

### Hardware and software requirements for a three-node configuration
{: #inst-hwt}

This configuration requires a minimum of four servers, either physical or virtual machines, three acting as a master and worker node (for example, `node1` acts as both `master1` and `worker1`), and one acting as load balancer.

| Node type | Number of servers (BM/VM) | CPU | RAM | Disk partition
|:---|:---:|:---:|:---:|:---
| Master/worker | 3 | 32 cores | 128 GB | 100GB for /[root] file system |
| | | | | Minimum of 400 GB mounted XFS file system for the installation path. This path is for the installer data storage on each node. Must be high-performance disk drive, such as SSD. |
| | | | | Minimum of 400 GB mounted XFS file system for the data path. The data path is for user data storage. This amount provides 400 GB usable space for user data with 3x replication. Depending on the user workload, more disk space might be required. |
| | | | | Optional: 200GB raw disk for the Docker devicemapper. If you do not provide this raw disk, you must have 600 GB minimum for the installation path. |
| Load balancer | 1 | Minimum 4 cores | 8GB | Minimum 100GB This minimum requirement for one load balancer is for clients using {{site.data.keyword.pm_full}}. It is not required for configurations where load balancing is handled by other providers, such as services hosted by Google or AWS. |

### Hardware and software requirements for a six-node configuration
{: #inst-hws}

This configuration requires a minimum of seven servers, either physical or virtual machines, three acting as `master` nodes, three acting as `worker` nodes, and one acting as load balancer.

| Node type | Number of servers (BM/VM) | CPU | RAM | Disk partition
|:---|:---:|:---:|:---:|:---
| Master | 3 | 16 cores | 32 GB | 100 GB for /[root] file system |
| | | | | 400 GB mounted XFS file system for the installation path. This path is for the installer data storage on each node. Must be high-performance disk drive, such as SSD. |
| | | | | 400 GB mounted XFS file system for the data path. The data path is for user data storage. This amount provides 500 GB usable space for user data with 3x replication. Depending on the user workload, more disk space might be required. |
| | | | | Optional: 200 GB raw disk for the Docker devicemapper. If you do not provide this raw disk, you must have 600 GB minimum for the installation path. |
| Worker | 3 | 16 cores | 128 GB | 100 GB for /[root] file system |
| | | | | 400 GB mounted XFS file system for the installation path. This path is for the installer data storage on each node. |
| | | | | 400 GB mounted XFS file system for the data path. The data path is for user data storage on each of the three worker nodes in the cluster. This amount provides 400 GB usable space for user data with 3x replication. Depending on the user workload, more disk space might be required. |
| | | | | Optional: 200 GB raw disk for the Docker devicemapper. If you do not provide this raw disk, you must have 600 GB minimum for the installation path. |

### (Optional) Db2 Warehouse requirements
{: #inst-hwd}

If you plan to deploy a Db2 Warehouse database in your {{site.data.keyword.icpfull_notm}} for Data cluster, you must create a dedicated worker node with the following specifications.

| Node type | Number of servers (BM/VM) | CPU | RAM | Disk partition
|:---|:---:|:---:|:---|:---
| Worker | 1 | 8 cores | 64 GB | TB storage is suitable for one database with the minimum configuration described. |
| | | | Minimum core-to-memory ratio: 1:8 | With multiple Db2 Warehouse pod deployments, or other workloads that use the same storage object class, more storage space is needed. |
| | | | Recommended core-to-memory ratio for improved performance: 1:16 | 5 TB as a starter is strongly recommended, depending on the amount of scoring that you will be performing. |

## Software requirements
{: #inst-sw}

Download the appropriate package, by part number, from [IBM Passport Advantage ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/software/passportadvantage/pao_customer.html){: new_window}.

Part numbers noted below differ based on whether you downloaded {{site.data.keyword.aios_full_notm}} for {{site.data.keyword.icpfull_notm}} for Data prior to April 16, 2019, or afterwards. Please be sure to select the right part number.
{: important}

1.  {{site.data.keyword.icpfull_notm}} for Data, running on {{site.data.keyword.icpfull_notm}}.

    - **_Prior to_** April 16, 2019: Download the standalone {{site.data.keyword.icpfull_notm}} for Data package, part number *CNY56EN*. This is a `.bin` file that includes both the {{site.data.keyword.icpfull_notm}} 3.1.2 platform, and {{site.data.keyword.icpfull_notm}} for Data 1.2 Enterprise Edition. The part number is for the {{site.data.keyword.icpfull_notm}} for Data Enterprise Edition package.

    - **_After_** April 16, 2019: Download {{site.data.keyword.icpfull_notm}} for Data Version 1.2.1.1, which is no longer bundled with the {{site.data.keyword.icpfull_notm}} platform, part number *CC11KML*.

1.  {{site.data.keyword.icpfull_notm}} for Data Watson Machine Learning Extension package

    - **_Prior to_** April 16, 2019 - Download the file associated with Version 1.2.0.1, part number *CC092EN*.

    - **_After_** April 16, 2019 - Download the file associated with Version 1.2.1, part number *CC0ENEN*.

1.  IBM Event Streams V2018.3.1 for Linux on x86 64-bit Multilingual

    - Download part number *CNXJ8ML*.

1.  IBM Db2 Warehouse for {{site.data.keyword.icpfull_notm}} for Data 1.2.1 (Optional)

    - **_Prior to_** April 16, 2019 - Download the file associated with Version 3.0, part number *CNY5DEN*.

    - **_After_** April 16, 2019 - Download the file associated with Version 3.3.0, part number *CC0EMEN*.

1.  {{site.data.keyword.aios_full_notm}} for {{site.data.keyword.icpfull_notm}} for Data, Linux 64-bit system

    - **_Prior to_** April 16, 2019 - Download the file associated with Version 1.0.1, part number *CNCZ1EN*.

    - **_After_** April 16, 2019 - Download the file associated with Version 1.0.2, part number *CC16SEN*.

<!---
MIKE: After April 16th change 3.1.0 to 3.1.2
## Installation artifacts
{: #inst-af}

1.  Download the latest starter installer build from [http://9.30.110.240:8088/job/icp-embedded-install-md5-test/ ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://9.30.110.240:8088/job/icp-embedded-install-md5-test/)

1.  Download the model installer:

    - [Deploy a Fyre cluster, build an embedded {{site.data.keyword.icpfull_notm}} installer with Zen, and install embedded {{site.data.keyword.icpfull_notm}} with Zen ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.ibm.com/PrivateCloud/InstallAndGo/wiki/How-to-Deploy-a-Fyre-Cluster,-Build-Embedded-ICP-installer-with-Zen,-and-Install-Embedded-ICP-with-Zen)

    OR

    - [Install or upgrade a module for an existing {{site.data.keyword.icpfull_notm}} environment ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.ibm.com/PrivateCloud/icp-embedded-installer/wiki/Install-Upgrade-a-Module-on-ICP4)

  Download the `installer.tar` file and untar it.

1.  Download the Watson Machine Learning model:

    - Find the latest build at [http://9.30.110.240:8088/job/WML-Helm-Chart/ ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://9.30.110.240:8088/job/WML-Helm-Chart/)

  Download the `wml_module.tar.gz` file.

--->

## Configuration requirements
{: #inst-conf}

The following configuration notes must be observed when installing {{site.data.keyword.icpfull_notm}} for Data.

- Public IP addresses of all cluster nodes must be static.
- Private IP addresses of all cluster nodes must be static. If an IP address is changing from one machine reboot to another, the system cannot be used.
- All cluster nodes must enable root login.
- All cluster nodes must have the same root password during installation time.
- The following ports must be opened on the Load Balancer node:

| Ports |  |  |  |  |
|:---:|:---:|:---:|:---:|:---:
| 8001 | 8443 | 9443 | 8500 | 8600 |
| 80 | 443 | 31843 | 32448 | 31962 |
| 31030 | 31031 | 30836 | 31002 | 32006 |

- If DB2 Warehouse is used, then the DB2 node port should also be opened on load balancer.

## I have **_already installed_** {{site.data.keyword.icpfull_notm}} for Data
{: #inst-exist}

If you already have an {{site.data.keyword.icpfull_notm}} for Data cluster installed, upgrade your embedded {{site.data.keyword.icpfull_notm}} and {{site.data.keyword.icpfull_notm}} for Data components by following the [Upgrading IBM Cloud Private for Data](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_1.2.1/com.ibm.icpdata.doc/zen/install/upgrade-overview.html) instructions. Ensure that you:

- Upgrade {{site.data.keyword.icpfull_notm}} from version 3.1.0 to 3.1.2
- Upgrade {{site.data.keyword.icpfull_notm}} for Data from version 1.2.0 to 1.2.1

Once the nodes are provisioned, continue with [Install the Watson Machine Learning package](#inst-wml) below.

## I have **_not yet installed_** {{site.data.keyword.icpfull_notm}} for Data
{: #inst-icp4d}

Review the [Overview of IBM Cloud Private for Data ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_1.2.1/com.ibm.icpdata.doc/zen/overview/overview.html) topic, in the IBM Knowledge Center.

Next, use automated scripts to prepare and install {{site.data.keyword.aios_short}} from scratch. Assume that you have a set of machines that have met the [hardware requirements](#inst-hw).

Scripts are optimized for a virtual private cloud within IBM SoftLayer.
{: note}

- Download the {{site.data.keyword.aios_short}} tarball and save it to the machine to be used as the `master1` node, for example, `/openscale`.

- Extract the automation scripts by running the following commands:

  ```bash
  tar -xzf <OpenScale.tar.gz file> utils/prepCluster.zip
  cd utils
  unzip prepCluster.zip
  cd install
  ```

- Follow the `README.md` instructions under the install directory to prepare, validate, and install {{site.data.keyword.icpfull_notm}} for Data, Watson Machine Learning, Event Streams, and {{site.data.keyword.aios_short}}. Optionally, refer to the [Db2 Warehouse install guide](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_1.2.0/com.ibm.icpdata.doc/zen/admin/download-db-pkg.html) to install Db2.

<!---

1.  Ensure that you have downloaded the installation image(s) to the machine with your master (`master-1`) node.

1.  SSH into the master (`master-1`) node of your cluster as root:

    ```bash
    ssh root@MASTER_1_IP
    ```

1.  Change to the file partition where you placed the installation file, for example: `/installer`.

1.  Run the `installOpenScale.sh` script. You can select one of three options to provision:

    - **3+1 servers**: load balancer + 3 master/worker nodes
    - **6+1 servers**: load balancer + 3 master + 3 worker nodes
    - **9+1 servers**: load balancer + 3 master + 6 worker nodes

Once the nodes are provisioned, continue with [Install the Watson Machine Learning package](#inst-wml) below.

--->

<!---

1.  Provision 6 + 1 hosts.

1.  Change the root password of all nodes to the same value.

1.  Modify `/etc/hosts` to include all nodes, for example:

    ```curl
    <server-01-IP> aios-icp4d-01.ibm.cloud aios-icp4d-01
    <server-02-IP> aios-icp4d-02.ibm.cloud aios-icp4d-02
    <server-03-IP> aios-icp4d-03.ibm.cloud aios-icp4d-03
    <server-04-IP> aios-icp4d-04.ibm.cloud aios-icp4d-04
    <server-05-IP> aios-icp4d-05.ibm.cloud aios-icp4d-05
    <server-06-IP> aios-icp4d-06.ibm.cloud aios-icp4d-06
    <server-07-IP> aios-icp4d-lb.ibm.cloud aios-icp4d-lb
    ```

1.  Configure SSH key password-less access from the first master node to all other nodes.

    - Generate ssh key in the first master node:

      `ssh-keygen -f /root/.ssh/id_rsa -q -N ""`

    - Add the key to the list of authorized keys:

      `cat ~/.ssh/id_rsa.pub | sudo tee -a ~/.ssh/authorized_keys`

    - Copy the public key to all other nodes:

      `ssh-copy-id -i /root/.ssh/id_rsa.pub root@[other node IP]`

    - Run `ssh root@[all nodes]` to make sure a password is not needed

1.  Sync your system time using the NTP server:

    `https://www.dyclassroom.com/reference-server/how-to-sync-linux-server-time-with-ntp-network-time-protocol-server`

    - Install NTP:

      `yum install ntp -y`

    - To enable NTP to start at boot, use the following command:

      `systemctl enable ntpd`

    - Start NTP:

      `systemctl start ntpd`

    - Sync time:

      `ntpdate -q 0.rhel.pool.ntp.org`

    - Restart NTP:

      `systemctl restart ntpd`

    - Check NTP statistics:

      `ntpstat`

    Or create a script, `ntp.sh`, and run the script:

      ```curl
      yum install ntp -y
      systemctl enable ntpd
      systemctl start ntpd
      ntpdate -q 0.rhel.pool.ntp.org
      systemctl restart ntpd
      ntpstat
      ```

    Or run:

      ```curl
      yum install ntp -y;systemctl enable ntpd;systemctl start ntpd;ntpdate -q 0.rhel.pool.ntp.org;systemctl restart ntpd;sleep 10;ntpstat
      ```

1.  Disable firewall on each node:

    ````curl
    systemctl stop firewalld
    systemctl disable firewalld
    ```

1.  Edit the `/etc/selinux/config` file and set to `permissive`. Set:

    ```curl
    SELINUX=permissive
    ```

    Reboot all systems:

    ```curl
    shutdown –r now
    ```

    Validate the change:

    ```curl
    getenforce
    ```

1.  To ensure that you do not yet have a partition allocated, run `lsblk`:

    ```curl
    lsblk

    NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    xvda    202:0    0  100G  0 disk
    ├─xvda1 202:1    0  256M  0 part /boot
    └─xvda2 202:2    0 99.8G  0 part /
    xvdb    202:16   0    2G  0 disk
    └─xvdb1 202:17   0    2G  0 part [SWAP]
    xvdc    202:32   0  500G  0 disk
    xvde    202:64   0  500G  0 disk

1.  Create a `disk.sh` script on all master / worker nodes

    ```curl
    #!/bin/bash
    if [[ $# -ne 2 ]]; then
      echo "Requires a disk name and mounted path name"
      echo "$(basename $0) <disk> <path>"
      exit 1
    fi
    set -e
    parted ${1} --script mklabel gpt
    parted ${1} --script mkpart primary '0%' '100%'
    sleep 1
    mkfs.xfs -f -n ftype=1 ${1}1
    mkdir -p ${2}
    echo "${1}1       ${2}              xfs     defaults,noatime    1 2" >> /etc/fstab
    mount ${2}
    exit 0
    ```

1.  Run `chmod +x disk.sh` on all master / worker nodes. Check to make sure the raw disks exist by running `lsblk` again

1.  Run `./disk.sh /dev/xvdc /ibm` on all master / worker nodes

1.  Run `./disk.sh /dev/svde /data` on all master / worker nodes

    OR

    Run all at once:

    ```curl
    ./disk.sh /dev/xvdc /ibm;./disk.sh /dev/xvde /data;lsblk
    ```

    Validate that `/etc/fstab` is correct:

    ```curl
    more /etc/fstab
    ```

    Two new entries should be there:

    ```curl
    /dev/xvdc1       /ibm              xfs     defaults,noatime    1 2
    /dev/xvde1       /data              xfs     defaults,noatime    1 2
    ```

1.  Now, run `lsblk` again to make sure the disk is partitioned:

    ```curl
    lsblk

    NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    xvda    202:0    0  100G  0 disk
    ├─xvda1 202:1    0  256M  0 part /boot
    └─xvda2 202:2    0 99.8G  0 part /
    xvdb    202:16   0    2G  0 disk
    └─xvdb1 202:17   0    2G  0 part [SWAP]
    xvdc    202:32   0  500G  0 disk
    └─xvdc1 202:33   0  500G  0 part /ibm
    xvde    202:64   0  500G  0 disk
    └─xvde1 202:65   0  500G  0 part /data

### Install load balancer
{: #inst-icplb}

1.  Run the following steps to install the load balancer

    ```curl
    yum install -y haproxy

    rm -rf /etc/haproxy/haproxy.cfg
    ```

1.  Create a new `/etc/haproxy/haproxy.cfg` file and add the content as directed in the Install guide. Replace the master private IP token with the actual private IP of three master nodes. An sample `haproxy.cfg` file from the install guide is shown here:

    ```curl
    # Example configuration for a possible web application.  See the
    # full configuration options online.
    #
    #   http://haproxy.1wt.eu/download/1.4/doc/configuration.txt
    #
    # Global settings
    global
      # To view messages in the /var/log/haproxy.log you need to:
      #
      # 1) Configure syslog to accept network log events.  This is done
      #    by adding the '-r' option to the SYSLOGD_OPTIONS in
      #    /etc/sysconfig/syslog.
      #
      # 2) Configure local2 events to go to the /var/log/haproxy.log
      #   file. A line similar to the following can be added to
      #   /etc/sysconfig/syslog.
      #
      #    local2.*                       /var/log/haproxy.log
      #
      log         127.0.0.1 local2

      chroot      /var/lib/haproxy
      pidfile     /var/run/haproxy.pid
      maxconn     4000
      user        haproxy
      group       haproxy
      daemon

    # 3) Turn on stats unix socket
      stats socket /var/lib/haproxy/stats
      # Common defaults that all the 'listen' and 'backend' sections
      # use, if not designated in their block.
    defaults
      mode                    http
      log                     global
      option                  httplog
      option                  dontlognull
      option http-server-close
      option                  redispatch
      retries                 3
      timeout http-request    10s
      timeout queue           1m
      timeout connect         10s
      timeout client          1m
      timeout server          1m
      timeout http-keep-alive 10s
      timeout check           10s
      maxconn                 3000

    frontend k8s-api
      bind *:8001
      mode tcp
      option tcplog
      use_backend k8s-api

    backend k8s-api
      mode tcp
      balance roundrobin
      server server1 <master-1-private-ip>:8001
      server server2 <master-2-private-ip>:8001
      server server3 <master-3-private-ip>:8001

    frontend dashboard
      bind *:8443
      mode tcp
      option tcplog
      use_backend dashboard

    backend dashboard
      mode tcp
      balance roundrobin
      server server1 <master-1-private-ip>:8443
      server server2 <master-2-private-ip>:8443
      server server3 <master-3-private-ip>:8443

    frontend auth
      bind *:9443
      mode tcp
      option tcplog
      use_backend auth

    backend auth
      mode tcp
      balance roundrobin
      server server1 <master-1-private-ip>:9443
      server server2 <master-2-private-ip>:9443
      server server3 <master-3-private-ip>:9443

    frontend registry
      bind *:8500
      mode tcp
      option tcplog
      use_backend registry

    backend registry
      mode tcp
      balance source
      server server1 <master-1-private-ip>:8500
      server server2 <master-2-private-ip>:8500
      server server3 <master-3-private-ip>:8500

    frontend registry-manager
      bind *:8600
      mode tcp
      option tcplog
      use_backend registry-manager

    backend registry-manager
      mode tcp
      balance roundrobin
      server server1 <master-1-private-ip>:8600
      server server2 <master-2-private-ip>:8600
      server server3 <master-3-private-ip>:8600

    frontend proxy-http
      bind *:80
      mode tcp
      option tcplog
      use_backend proxy-http

    backend proxy-http
      mode tcp
      balance roundrobin
      server server1 <master-1-private-ip>:80
      server server2 <master-2-private-ip>:80

    frontend proxy-https
      bind *:443
      mode tcp
      option tcplog
      use_backend proxy-https

    backend proxy-https
      mode tcp
      balance roundrobin
      server server1 <master-1-private-ip>:443
      server server2 <master-2-private-ip>:443

    frontend zen-board
      bind *:31843
      mode tcp
      option tcplog
      use_backend zen-board

    backend zen-board
      mode tcp
      balance roundrobin
      server server1 <master-1-private-ip>:31843
      server server2 <master-2-private-ip>:31843
      server server3 <master-3-private-ip>:31843
    ```

    `[root@aios-icp4d-lb haproxy]# sed -i 's#<master-1-private-ip>#10.187.210.164#g' haproxy.cfg`

    `[root@aios-icp4d-lb haproxy]# sed -i 's#<master-2-private-ip>#10.187.210.166#g' haproxy.cfg`

    `[root@aios-icp4d-lb haproxy]# sed -i 's#<master-3-private-ip>#10.187.210.140#g' haproxy.cfg`

1.  Start haproxy:

    ```curl
    systemctl start haproxy
    ```

1.  Enable haproxy:

    ```curl
    systemctl enable haproxy
    ```

1.  Check status:

    ```curl
    systemctl status -l haproxy

    haproxy.service - HAProxy Load Balancer
      Loaded: loaded (/usr/lib/systemd/system/haproxy.service; enabled; vendor preset: disabled)
      Active: active (running) since Sun 2018-09-30 20:46:34 CDT; 28s ago
    Main PID: 7453 (haproxy-systemd)
      CGroup: /system.slice/haproxy.service
        ├─7453 /usr/sbin/haproxy-systemd-wrapper -f /etc/haproxy/haproxy.cfg -p /run/haproxy.pid
        ├─7454 /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg -p /run/haproxy.pid -Ds
        └─7455 /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg -p /run/haproxy.pid -Ds

    Sep 30 20:46:34 aios-icp4d-lb.ibm.cloud systemd[1]: Started HAProxy Load Balancer.
    Sep 30 20:46:34 aios-icp4d-lb.ibm.cloud systemd[1]: Starting HAProxy Load Balancer...
    Sep 30 20:46:34 aios-icp4d-lb.ibm.cloud haproxy-systemd-wrapper[7453]: haproxy-systemd-wrapper: executing /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg -p /run/haproxy.pid -Ds
    ```

### Test load balancer
{: #inst-icpte}

See [Setting up an external load balancer ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSBS6K_2.1.0.3/installing/set_loadbalancer.html) and [How to test the load balancer![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.ibm.com/PrivateCloud/icp-embedded-installer/wiki/How-to-test-the-load-balancer) for more information.

1.  Install ncat program if it does not exist on the system:

    ```curl
    yum install -y nc
    ```

1.  On three master nodes, issue command:

    ```curl
    ncat -lkp 8600
    ```

1.  On a separate system, issue command:

    ```curl
    echo 1 | ncat <load_balancer_ip> 8600
    ```

    multiple times. Make sure the console from three master nodes receive the messages on a round-robin fashion.

1.  Repeat steps 2 and 3 for other ports (443, 80, 8001, 8443, 8500, 9443, 31843) to make sure the load balance also works.

## Prepare installation configuration file `wdp.conf`
{: #inst-icpco}

1.  Create the file `/ibm/wdp.conf`

1.  Add the following lines to the file:

    ```curl
    ssh_key=/root/.ssh/id_rsa
    master_node_1=<master1 ip>
    master_node_path_1=/ibm
    master_node_2=<master2 ip>
    master_node_path_2=/ibm
    master_node_3=<master3 ip>
    master_node_path_3=/ibm
    worker_node_1=<worker1 ip>
    worker_node_path_1=/ibm
    worker_node_data_1=/data
    worker_node_2=<worker2 ip>
    worker_node_path_2=/ibm
    worker_node_data_2=/data
    worker_node_3=<worker3 ip>
    worker_node_path_3=/ibm
    worker_node_data_3=/data
    virtual_ip_address_1=<loadbalance ip>
    virtual_ip_address_2=<loadbalance ip>
    ssh_port=22

  Replace the corresponding IPs with the actual private IPs on master or worker nodes. Replace the loadbalance IP with a loadbalance public IP.

1.  Install `screen` on the master 1 node:

    ```curl
    yum install -y screen
    ```

1.  Issue the `screen` command:

    ```curl
    screen
    ```

1.  Run `chmod +x installer.x86_64.231`

1.  Run the installation program:

    ```curl
    ./installer.x86_64.231 --load-balancer

    ==> Type Y to use wdp.conf file
    ==> Type A to accept license
    ```

1.  If the console gets disconnected, log back into the master server in the `/ibm` location:

    ```curl
    cd /ibm

    screen -ls

    screen -d -r [screen section number, for example: 3687]
    ```

--->

## Install the Watson Machine Learning package
{: #inst-wml}

Follow the instructions to install the [Watson Machine Learning add-on ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/admin/extend-ai-analytics.html#extend-ai-analytics__wml), in the IBM Knowledge Center.

At the end of the Watson Machine Learning module installation into ICP4D, add the following lines to `/etc/haproxy/haproxy.cfg` on the load balancer system:

  ```bash
  frontend wml
      bind *:31002
      mode tcp
      option tcplog
      use_backend wml

  backend wml
      mode tcp
      balance roundrobin
      server server1 <master01-IP>:31002
      server server2 <master02-IP>:31002
      server server3 <master03-IP>:31002

  frontend wml-envoy
      bind *:32006
      mode tcp
      option tcplog
      use_backend wml-envoy

  backend wml-envoy
      mode tcp
      balance roundrobin
      server server1 <master01-IP>:32006
      server server2 <master02-IP>:32006
      server server3 <master03-IP>:32006
  ```

  Change the IP address to the IP address of all the cluster master nodes.
  {: note}

  The server name in this configuration file always starts from `server1`, `server2`, `server3`, etc.
  {: note}

After saving the above changes, run the following command, for the changes to take effect:

  ```bash
  systemctl restart haproxy
  systemctl status -l haproxy
  ```

Then confirm the command output has no error - the following is a sample reference output:

  ```bash
  haproxy.service - HAProxy Load Balancer
   Loaded: loaded (/usr/lib/systemd/system/haproxy.service; enabled; vendor preset: disabled)
   Active: active (running) since Mon 2018-12-10 09:48:06 CST; 6ms ago
 Main PID: 73659 (haproxy-systemd)
   CGroup: /system.slice/haproxy.service
           ├─73659 /usr/sbin/haproxy-systemd-wrapper -f /etc/haproxy/haproxy.cfg -p /run/haproxy.pid
           └─73661 /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg -p /run/haproxy.pid -Ds

  Dec 10 09:48:06 yssd.yong.cloud systemd[1]: Started HAProxy Load Balancer.
  Dec 10 09:48:06 yssd.yong.cloud systemd[1]: Starting HAProxy Load Balancer...
  Dec 10 09:48:06 yssd.yong.cloud haproxy-systemd-wrapper[73659]: haproxy-systemd-wrapper: executing /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg -p /run/haproxy.pid -Ds
  ```

<!---

1.  Download the `installer.tgz` package from [https://github.ibm.com/PrivateCloud/icp-embedded-installer/blob/sequenced-installer/Installer/InstallPackage/utils/installer.tgz](https://github.ibm.com/PrivateCloud/icp-embedded-installer/blob/sequenced-installer/Installer/InstallPackage/utils/installer.tgz)

1.  Download the modules to be installed from [http://9.30.110.240:8088/job/icp-embedded-install-v2/](http://9.30.110.240:8088/job/icp-embedded-install-v2/).

1.  Untar the `installer.tgz` to the same folder where the module's files are located.

1.  Call the script to install a single module:

    ```curl
    # ./installZEN.sh <module's filename>
    ```

    OR

    Install all modules at once by changing the `PACKAGES` variable inside the `installZEN.sh` file, and calling the script without any parameter. The order of the packages here will define the order of the packages installation. A sample is provided with all the modules.

  The script will monitor the progress of each module installation. Since the deploy time can change depending on the hardware, and to avoid long wait times, a time limit was set to finish the monitor after 5 minutes. Be aware that after the script finish some pods can be still in pending state.

See [Install or Upgrade a module on ICP](https://github.ibm.com/PrivateCloud/icp-embedded-installer/wiki/Install-Upgrade-a-Module-on-ICP4) for more information.

### Troubleshoot installation issues
{: #inst-icpts}

The install log location is `/ibm/InstallPackage/tmp`.

    ```curl
    cat attach.sh

    #!/usr/bin/env bash

    #check the last 10 lines of docker logs for failure
    docker_logs=$(docker logs --tail 10 dp-installer | grep -Ei 'fail' | grep -Ei 'retry' | grep -Ei 'skip')

    if [ -n "${docker_logs}" ]; then
      echo "${docker_logs}"
    fi

    docker attach --sig-proxy=false --detach-keys 'ctrl-c' dp-installer
    setterm -cursor on

    disabled_management_services: ["istio", "vulnerability-advisor", "custom-metrics-adapter"]

    cluster_lb_address: 169.62.226.21
    proxy_lb_address: 169.62.226.21
    ```

  See [Installer issue information required](https://github.ibm.com/PrivateCloud/icp-embedded-installer/wiki/Installer-issue-information-required) for more details.

### Uninstall
{: #inst-icpu}

To uninstall, run:

  ```curl
  /dp/utils/dpctl playbook --tasks /dp/utils/tasks/uninstall.yaml --hosts /dp/ibm-cp-app/cluster/hosts -u root -p temp4now
  ```

--->

## (Optional) Install the IBM Db2 Warehouse package
{: #inst-db2}

Follow the instructions for [Downloading the database installation package ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/admin/download-db-pkg.html#download-db2-warehouse-pkg), in the IBM Knowledge Center.

## Log into your {{site.data.keyword.icpfull_notm}} for Data cluster
{: #log-cluster}

Enter the following command:

`cloudctl login`

When prompted, enter your ICP Admin username and password.

## Install IBM Event Streams V2018.3.1 for Linux and {{site.data.keyword.aios_full_notm}} for {{site.data.keyword.icpfull_notm}}
{: #inst-es-aios}

### Install Event Streams
{: #inst-es}

1.  Copy the IBM Event Streams V2018.3.1 for Linux on x86 64-bit Multilingual tarball to a directory on the {{site.data.keyword.icpfull_notm}} for Data cluster `master-1 node`, for example, `/ibm/ES`.

1.  Untar the {{site.data.keyword.aios_full_notm}} for {{site.data.keyword.icpfull_notm}} 1.0.2 tarball to a directory on your {{site.data.keyword.icpfull_notm}} for Data cluster `master-1 node`, for example, `/ibm/AIOS`.

1.  Log into your docker registry and {{site.data.keyword.aios_full_notm}} cluster from a command line window.

1.  Install Event Streams from your {{site.data.keyword.icpfull_notm}} for Data cluster `master-1 node` by using the `install_es.sh` package in the {{site.data.keyword.aios_short}} tarball, for example:

    ```bash
    cd /ibm/AIOS
    ./install_es.sh -f /ibm/ES/[<Event_Streams_tarball_file_name>]
    ```

1.  When `install_es.sh` has finished executing, the following message will display. Complete the steps outlined in the message before proceeding to the next step:

    ```bash
    Follow the steps below to expose the ports for Event Stream through the HAProxy load balancer:

    1. Append the content of `${HAPROXY_OUTPUT}` to `/etc/haproxy/haproxy.cfg` on `${LOAD_BALANCER_IP}`

    2. Run `systemctl restart haproxy` on `${LOAD_BALANCER_IP}` to restart the HAProxy load balancer.

    If another load balancer is used, configure it to expose ports 31703, 31105, 31094, 32180, and 32036 for Event Stream to the master nodes.
    ```

### Install {{site.data.keyword.aios_full_notm}}
{: #inst-aios}

1.  Install {{site.data.keyword.aios_short}}.

    If your cluster has not been installed using an embedded {{site.data.keyword.icpfull_notm}} for Data installation, you need to perform the following steps:
    {: important}

    - Update the environment variable settings in the `common.sh` file included in the {{site.data.keyword.aios_short}} tarball.

    - If you are using manual storage provisioning, you must manually create persistent volumes required for the {{site.data.keyword.aios_short}} components.

        - Customize the `utils/etcd-pvc-template.yaml` file included in the {{site.data.keyword.aios_short}} tarball for your environment. Replace the `nfs` section in the template if you are using another storage type.

          - To use NFS volumes:

            - Replace the `NFS_SERVER_IP` with your NFS host IP address

            - Replace `/data/aios-etcd-0`, `/data/aios-etcd-1`, and `/data/aios-etcd-2`, if your NFS mount point is different.

            - Run `kubectl create namespace aiopenscale`

            - Run `kubectl -n aiopenscale create -f etcd-pvc-template.yaml` to create `PersistentVolume` and `PersistentVolumeClaim`

    - If you are using `DynamicProvisioning` with a `StorageClass`, replace `oketi-gluster` with your `StorageClass` name in the `common.sh` file.

    Run the installation:

    ```bash
    ./install_aios.sh
    ```

  The installation will prompt you to read and accept the license agreement, {{site.data.keyword.icpfull_notm}} for Data Admin `username` and `password`, {{site.data.keyword.icpfull_notm}} Admin `username` and `password`, Event Streams release name, and Event Streams namespace.

  Default values are provided wherever possible. You should use the default values if you follow the installation steps for {{site.data.keyword.icpfull_notm}} for Data, Watson Machine Learning, and Event Streams, as defined in this document.

## Verifying your installation
{: #inst-po}

- Log into the {{site.data.keyword.icpfull_notm}} for Data [Management Console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_2.1.0.3/manage_cluster/cfc_gui.html), then go to the *Add-ons* page by clicking the icon in the upper-right corner of the screen.

  OR

- Type `https://[Load Balancer IP]:31843/zen/#/addons`, and click the {{site.data.keyword.aios_short}} add-on to open the {{site.data.keyword.aios_short}} UI.

  The {{site.data.keyword.aios_short}} UI can also be launched using `https://[Load Balancer IP]:31843/aiopenscale` after logging into the {{site.data.keyword.aios_full_notm}} for {{site.data.keyword.icpfull_notm}} UI.

## Uninstallation steps
{: #inst-un}

1.  Go to the directory from where you installed {{site.data.keyword.aios_short}}, for example `ibm/aios`, on the {{site.data.keyword.icpfull_notm}} for Data cluster `master-1 node` host.

1.  Run `./uninstall_aios.sh`

The uninstallation will prompt for {{site.data.keyword.icpfull_notm}} Admin `username` and `password`.

## Next steps
{: #inst-next}

Use the {{site.data.keyword.aios_short}} tool to monitor your AI models for bias and accuracy.

- To learn more about the {{site.data.keyword.aios_short}} service, see [About](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-abt-about).
- To see how it works for yourself, follow the steps in the [Getting Started](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-gs-get-started) tutorial.
