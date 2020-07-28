# ansible-confluence

Ansible role for install and configure [confluence](https://www.atlassian.com/software/confluence)

Limitation
----------

1. This role not install `java` you must first install them yourself
2. If you want to use revers proxy `apache` or `nginx` you must first install them yourself
3. If you want to use an external DB such as (Mysql/PostgreSQL) install the selected DB before the run role
4. This role not manage selinux permission

Requirements
------------
Tested on RHEL 7, CentOS 7/8

* ansible 2.8 or above
* java SDK 8 or 11

Role Variables
--------------
**It is not necessary to use all these variable blocks, you can use only the config options you really need.** 

Available variables are be listed below, along with default values. See [defaults/main.yml](defaults/main.yml).

You can change all variables by group_vars or host_vars

| Variable name | Required* | Description | Default Value |
| :---: | :---: | :---: | :---: |
| `confluence_version` | **Yes** | Version of the installing confluence software | 7.4.1 | 
| `confluence_manage_user` | **No** | Should this role manage the confluence user? | true | 
| `confluence_user` | **No** | OS user name | confluence | 
| `confluence_group` | **No** | OS group name | confluence | 
| `confluence_session_timeout` | **No** | session duration | 300 |
| `confluence_bin_path` | **No** | confluence binary dir | /opt/atlassian/confluence | 
| `confluence_data_path` | **No** | confluence data dir | /opt/atlassian/application-data/confluence | 
| `confluence_jvm_minimum_memory` | **No**   | JVM min memory | 1024m | 
| `confluence_jvm_maximum_memory` | **No** | JVM max memory | 1024m | 

If you want use reverse proxy for confluence you must set additional setting

| Variable name | Required* | Description | Default Value |
| :---: | :---: | :---: | :---: |
| `confluence_catalina_connector_proxyname` | **No** | log driver for kanboard | "" |
| `confluence_catalina_connector_scheme` | **No** | used protocol | http |
| `confluence_catalina_connector_proxyport` | **No** | used proxy port | depends on scheme(80 or 443) |
| `confluence_catalina_connector_secure` | **No** | used secure connection | depends on scheme |
| `confluence_catalina_context_path` | **No** | web path for confluence | / |

****Required*** - if "yes", you need to set this parameter under your conditions.

Dependencies
------------
 
Example Playbook
------------

```yml
- name: Install confuence
  hosts: 
    - confuence.example.com
  become: yes
  become_method: sudo
  roles:
    - ansible-confuence
  vars:
    confuence_version: "7.5.2"
    confuence_manage_user: true
    confuence_user: confuence
    confluence_jvm_maximum_memory: "2048m"
    confluence_catalina_connector_proxyname: wiki.example.com
    confluence_catalina_connector_scheme: "https"
    confluence_data_path: "/data/confluence"
```