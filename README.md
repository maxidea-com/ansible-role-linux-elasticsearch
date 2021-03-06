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
Elasticsearch is the living heart of what is today’s the most popular log analytics platform — the ELK Stack (Elasticsearch, Logstash and Kibana). Elasticsearch’s role is so central that it has become synonymous with the name of the stack itself. Elasticsearch is a search engine based on the Lucene library. It provides a distributed, multitenant-capable full-text search engine with an HTTP web interface and schema-free JSON documents. Completely open source and built with Java, Elasticsearch is a NoSQL database. That means it stores data in an unstructured way and that you cannot use SQL to query it. In the context of data analysis, Elasticsearch is used together with the other components in the ELK Stack, Logstash and Kibana, and plays the role of data indexing and storage.

## Requirements
### Operating systems
This Ansible role installs Elasticsearch on linux operating system, including establishing a filesystem structure and server configuration with some common operational features.  This role will work on the following operating systems:

  * CentOS 7

### Elasticsearch versions

The following list of supported the Elasticsearch releases:

* Elasticsearch 5.6+, 6.8+, 7.1+

## Role variables
### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:

##### General parameters
* `elastic_cluster`: Specify name for your cluster name.
* `elastic_version`: Specify the Elasticsearch version.
* `elastic_path`: Specify the Elasticsearch data directory.
* `elastic_auth`: A boolean value, Enable or Disable authentication.
* `elastic_pass`: Authorization password.
* `elastic_https`: A boolean value, whether Encrypting HTTP client communications.
* `elastic_heap_size`: Specify the maximum memory allocation pool for a Java virtual machine.
* `elastic_memory_lock`: A boolean value, whether lock the process address space into memory on startup.
* `elastic_node_type`: Type of nodes: default, master, data, ingest and coordinat.

##### Listen port
* `elastic_port_rest`: Elasticsearch REST port.
* `elastic_port_transport`: Elasticsearch transport port ragne.
* `elastic_port_exporter`: Prometheus Elasticsearch Exporter port.

##### Server System Variables
* `elastic_arg.action_destructive_requires_name`: Restricts deletions to specific names, instead of allowing the special _all or wildcard options.
* `elastic_arg.cluster_max_shards_per_node`: Controls the number of shards allowed in the cluster per data node.
* `elastic_arg.http_compression`: Compression when possible with Accept-Encoding.
* `elastic_arg.http_cors_enabled`: Enable or disable cross-origin resource sharing.
* `elastic_arg.http_cors_allow_methods`: Which methods to allow.

##### Service Mesh
* `environments`: Define the service environment.
* `tags`: Define the service custom label.
* `exporter_is_install`: Whether to install prometheus exporter.
* `consul_public_register`: Whether register a exporter service with public consul client.
* `consul_public_exporter_token`: Public Consul client ACL token.
* `consul_public_http_prot`: The consul Hypertext Transfer Protocol.
* `consul_public_clients`: List of public consul clients.
* `consul_public_http_port`: The consul HTTP API port.

### Other parameters
There are some variables in vars/main.yml:

## Dependencies
- Ansible versions >= 2.8
- Python >= 2.7.5

## Example

### Hosts inventory file
See tests/inventory for an example.

    [syslog]
    node01 ansible_host='192.168.1.10'
    node02 ansible_host='192.168.1.11'
    node03 ansible_host='192.168.1.12'

    [syslog:vars]
    elastic_cluster='syslog'
    elastic_version='7.6.2'

### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: all
  roles:
     - role: ansible-role-linux-elasticsearch
       elastic_cluster: 'syslog'
```

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`

```yaml
elastic_cluster: 'syslog'
elastic_version: '7.6.2'
elastic_path: '/data'
elastic_auth: false
elastic_pass: 'password'
elastic_https: false
elastic_heap_size: '3g'
elastic_memory_lock: false
elastic_node_type: 'default'
elastic_port_rest: '9200'
elastic_port_transport: '9300'
elastic_port_exporter: '9108'
elastic_arg:
  action_destructive_requires_name: true
  cluster_max_shards_per_node: '10000'
  http_compression: true
  http_cors_enabled: true
  http_cors_allow_methods: 'HEAD, GET, POST, PUT, DELETE'
environments: 'Development'
tags:
  subscription: 'default'
  owner: 'nobody'
  department: 'Infrastructure'
  organization: 'The Company'
  region: 'IDC01'
exporter_is_install: false
consul_public_register: false
consul_public_exporter_token: '00000000-0000-0000-0000-000000000000'
consul_public_http_prot: 'https'
consul_public_http_port: '8500'
consul_public_clients:
  - '127.0.0.1'
```

## License
![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.
