# 개요
일반적인 서버(PC나 노트북도 가능)는 Network Boot을 지원한다.
이때 subnet에 존재하는 DHCP 서버에게 ip를 획득하고 ftp를 통해 OS image를 받아서 kickstart를 통해 자동으로 설치가 가능하다.
(작성중)

# kickstar 파일
아래 파일은 호스트별로 만든다.
```
url --url ftp://10.220.13.62/pub/
#platform=x86, AMD64, 또는 Intel EM64T
#version=DEVEL
# Install OS instead of upgrade
install
# Firewall configuration
firewall --disabled
# Use CDROM installation media
cdrom
# Network information
network --device eth2 --onboot yes --hostname hadoop45 --bootproto static --ip 10.220.13.55 --netmask 255.255.255.0
network --device eth0 --onboot yes --bootproto static --ip 10.220.19.55 --netmask 255.255.255.0 --gateway 10.220.19.1
# Root password
rootpw --iscrypted $1$JRtGFZUz$gtU9uUsfW0dSogZd5.....
# System authorization information
auth  --useshadow  --passalgo=md5
# Use text mode install
text
# System keyboard
keyboard ko
# System language
lang ko_KR
# SELinux configuration
selinux --disabled
# Do not configure the X Window System
skipx
# Installation logging level
logging --level=info
# Reboot after installation
reboot
# System timezone
timezone  Asia/Seoul
# System bootloader configuration
bootloader --location=mbr
# Clear the Master Boot Record
zerombr
# Partition clearing information
clearpart --all --initlabel
# Disk partitioning information
 
# edit this
# Hadoop Masters
part /boot --fstype="ext4" --ondisk=sda --label=/boot --size=500
part swap --fstype="swap" --ondisk=sda --label=/swap --size=5000
part / --fstype="ext4" --ondisk=sda --label=/ --size=21000
part /data1 --fstype="ext4" --grow --label=/data1 --ondisk=sda --size=500000 --maxsize=3000000 --fsoptions="noatime,nodiratime,noacl,data=writeback,barrier=0,nobh,errors=remount-ro"
part /data2 --fstype="ext4" --grow --label=/data2 --ondisk=sdb --size=500000 --maxsize=3000000 --fsoptions="noatime,nodiratime,noacl,data=writeback,barrier=0,nobh,errors=remount-ro"
part /data3 --fstype="ext4" --grow --label=/data3 --ondisk=sdc --size=500000 --maxsize=3000000 --fsoptions="noatime,nodiratime,noacl,data=writeback,barrier=0,nobh,errors=remount-ro"
part /data4 --fstype="ext4" --grow --label=/data4 --ondisk=sdd --size=500000 --maxsize=3000000 --fsoptions="noatime,nodiratime,noacl,data=writeback,barrier=0,nobh,errors=remount-ro"
 
 
 
%packages --ignoremissing
@core
@base
 
yum-utils
ntpd
dialog
ltrace
sudo
bzip2
kernel-devel
kernel-headers
-ipw2100-firmware
-ipw2200-firmware
-ivtv-firmware
%end
 
%post
 
 
%end
```

# gen scripts
```
MASTER_HOST_NAME="hadoop1"
MASTER_HOST_IP="10.220.13.62"
MASTER_DEVICE_NAME="eth2"
SUB_NET_IP="10.220.13.0"
ROOT_PASSWD="ndap1234~"
DHCP_START_IP=10.220.13.150
DHCP_END_IP=10.220.13.244
 
 
# kickstart info
# HOST_NAME have to be first element
# watch out white space !!!
 
export HOST_MAC="
server2/1c-26-3d-48-5c-64/10.220.13.12/10.220.19.12
....
"
  
  
 
echo "test_host" > fHOST_NAME
echo "xx-xx-xx-xx-xx-xx" > fETH0_MAC_ADDRESS
echo "network --device eth2 --onboot yes --hostname hadoopXX --bootproto static --ip 10.220.13.XX --netmask 255.255.255.0" > fNETWORK_SETTING
echo "network --device eth0 --onboot yes --bootproto static --ip 10.220.19.XX --netmask 255.255.255.0 --gateway 10.220.19.1" > fNETWORK_SETTING2
 
for line in $HOST_MAC; do
  S1=`echo $line | cut -d'/' -f1`
  S2=`echo $line | cut -d'/' -f2`
  S3=`echo $line | cut -d'/' -f3`
  S4=`echo $line | cut -d'/' -f4`
  echo $S1 >> fHOST_NAME
  echo $S2 >> fETH0_MAC_ADDRESS
  echo "network --device eth2 --onboot yes --hostname $S1 --bootproto static --ip $S3 --netmask 255.255.255.0" >> fNETWORK_SETTING
  echo "network --device eth0 --onboot yes --bootproto static --ip $S4 --netmask 255.255.255.0 --gateway 10.220.19.1" >> fNETWORK_SETTING2
   
done
export HOST_NAME=`cat fHOST_NAME`
export ETH0_MAC_ADDRESS=`cat fETH0_MAC_ADDRESS`
export NETWORK_SETTING=`cat fNETWORK_SETTING`
export NETWORK_SETTING2=`cat fNETWORK_SETTING2`
 
export ACTIVE_ELEM="
ETH0_MAC_ADDRESS
NETWORK_SETTING
NETWORK_SETTING2
"
 
  
export PART_01=""
 
export PART_02=""
 
export PART_03=""
 
#PART_04="
#part / --fstype="ext4" --ondisk=sda --size=30000
#"
  
PART_05=""
PART_06=""
PART_07=""
PART_08=""
PART_09=""
```

참고 : https://github.com/gigsda/os_install-helper_for_ndap
