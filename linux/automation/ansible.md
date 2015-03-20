# Introduction

Model-driven configuration management, multi-node deployment/orchestration, and remote task execution system. Uses SSH by default, so there is no special software has to be installed on the nodes you manage. Ansible can be extended in any language. Note: The default branch is the development branch which many people run directly from checkout, if you need a stable version, see the release-XX branches, tags, or ansible.cc/releases.

[http://ansible.cc/]

# Quick start

## Install

EPEL
{code}
# yum install ansible
{code}

or

PIP
{code}
# pip-python install ansible
{code}

## Configuration

1. /etc/ansible/hosts

2. Set up SSH agent to avoid retyping passwords:
{code}
$ ssh-agent bash
$ ssh-add ~/.ssh/id_rsa
{code}
{info}
Passwordless SSH를 설정해두면 ansible 커맨드 사용 시 편리합니다.

{code}
# ssh-keygen -t rsa
# ssh-copy-id root@targt_host
{code}
{info}

# Hosts and Groups

The format for /etc/ansible/hosts is an INI format and looks like this:
{code}
mail.example.com

[webservers]
foo.example.com
bar.example.com

[dbservers]
one.example.com
two.example.com
three.example.com
{code}

그룹을 지정한 경우:
{code}
# ansible dbservers ...
{code}

호스트로 지정한 경우:
{code}
# ansible one.example.com -m ping
{code}

몇몇 호스트들로 지정한 경우:
{code}
# ansible one.example.com:two.example.com -m ping
{code}

h1. Basic usage
{code}
# ansible <pattern_goes_here> -m <module_name> -a <arguments>
{code}

# Examples

/etc/ansible/hosts
{code}
[kdap]
hadoop[1:52]

[mysql]
hadoop28

{code}

## 'CmdAllServer' 스크립트 구현

'hadoop' 호스트 그룹에 속한 서버에 커맨드를 실행하고 결과를 받아온다.
{code}
$  ansible kdap -a "/bin/echo hello"

hadoop12 | success | rc=0 >>
hello

hadoop13 | success | rc=0 >>
hello

hadoop11 | success | rc=0 >>
hello

hadoop10 | success | rc=0 >>
hello

......
{code}

# Ansible Modules

[http://ansible.cc/docs/modules.html]

# Playbooks

[http://ansible.cc/docs/playbooks.html]

# Ansible & Hadoop

* [https://github.com/analytically/hadoop-ansible]
* [https://github.com/jkleint/ansible-hadoop]
* [Using Ansible to Secure Cloudera Manager Installation on a Hadoop Cluster|http://www.pythian.com/blog/using-ansible-to-secure-cloudera-manager-installation-on-a-hadoop-cluster]
* [https://github.com/ansible/ansible-examples/tree/master/hadoop]

# Ansible Tutorial

[https://github.com/leucos/ansible-tuto]

# Reference

* [https://github.com/dsander/vagrant-ansible]
* [http://jpmens.net/2012/06/06/configuration-management-with-ansible/]
* [http://deview.kr/2014/session?seq=15]
* Deploying with Vagrant and Ansible, [https://speakerdeck.com/yeukhon/deploying-with-vagrant-and-ansible]
