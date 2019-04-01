![](https://img.shields.io/badge/Ansible-elasticsearch-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes,  should not be used in production environments.__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_elasticsearch.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [Operating systems](#operating-systems)
  * [Elasticsearch Versions](#Elasticsearch-versions)
- [ Role variables](#Role-variables)
  * [Minimal Configuration](#minimal-configuration)
  * [Main Configuration](#Main-parameters)
  * [Other Configuration](#Other-parameters)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Hosts inventory file](#Hosts-inventory-file)
  * [Vars in role configuration](#vars-in-role-configuration)
  * [Combination of group vars and playbook](#combination-of-group-vars-and-playbook)
- [License](#license)
- [Author Information](#author-information)
- [Contributors](#Contributors)

## Overview
This Ansible role installs Elasticsearch on linux operating system, including establishing a filesystem structure and server configuration with some common operational features.

## Requirements
### Operating systems
This role will work on the following operating systems:

  * CentOS 7

### Elasticsearch versions

The following list of supported the Elasticsearch releases:

* Elasticsearch 2, 5

## Role variables
### Minimal configuration

In order to get the Elasticsearch running, you'll have to define the following properties before executing the role:

* `elasticsearch_cluster_name`: Specify name for your cluster name.
* `elasticsearch_version`: Specify the Elasticsearch version.

### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:

##### General parameters
* `elasticsearch_path`: Specify the Elasticsearch data directory.
* `elasticsearch_selinux`: SELinux security policy.

##### Service Mesh
* `consul_is_register`: Whether register a client service with consul.
* `consul_exporter_token`: Consul client ACL token.
* `consul_clients`: List of consul clients.
* `consul_http_port`: The consul HTTP API port.

##### Listen port
* `elasticsearch_port_arg.rest`: Elasticsearch REST port.
* `elasticsearch_port_arg.node`: Elasticsearch nodes communication port.
* `elasticsearch_port_arg.exporter`: Prometheus Elasticsearch Exporter port.

##### Server System Variables
* `elasticsearch_arg.action_destructive_requires_name`: Restricts deletions to specific names, instead of allowing the special _all or wildcard options.
* `elasticsearch_arg.bootstrap_memory_lock`: Lock the process address space into RAM.
* `elasticsearch_arg.es_heap_size`: Specify the maximum memory allocation pool for a Java virtual machine.

### Other parameters
There are some variables in vars/main.yml:

## Dependencies
There are no dependencies on other roles.

## Example

### Hosts inventory file
See tests/inventory for an example.

    node01 ansible_host='192.168.1.10' elasticsearch_cluster_name='graylog'
    node02 ansible_host='192.168.1.11' elasticsearch_cluster_name='graylog'
    node03 ansible_host='192.168.1.12' elasticsearch_cluster_name='graylog'

### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - role: ansible-role-linux-elasticsearch
           elasticsearch_cluster_name: 'graylog'

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`

    elasticsearch_cluster_name: 'graylog'
    elasticsearch_version: '5'
    elasticsearch_path: '/data'
    elasticsearch_selinux: 'false'
    consul_is_register: false
    consul_exporter_token: '00000000-0000-0000-0000-000000000000'
    consul_clients: 'localhost'
    consul_http_port: '8500'
    elasticsearch_port_arg.rest: '9200'
    elasticsearch_port_arg.node: '9300'
    elasticsearch_port_arg.exporter: '9108'
    elasticsearch_arg.action_destructive_requires_name: true
    elasticsearch_arg.bootstrap_memory_lock: false
    elasticsearch_arg.es_heap_size: '4'

## License
![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.
