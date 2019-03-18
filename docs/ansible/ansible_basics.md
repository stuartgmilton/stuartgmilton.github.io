---
layout: default
title: Ansible Basics
parent: Ansible
nav_order: 9
---

# Ansible Basics

#### The Static Inventory File
Ansible works against multiple systems in your infrastructure at the same time. It does this by selecting portions of systems listed in Ansible’s inventory. The name of a group is enclosed in square brackets []. Server names can be their DNS names or IP addresses.  Not only is this inventory configurable, but you can also use multiple inventory files at the same time and pull inventory from dynamic or cloud sources or different formats (YAML, ini, etc).  An example Inventory is shown below, groups are surrounded by square brackets, and hosts are listed under each group.  This Inventory is in the ini format.

```bash
[proxy]
server0

[proxy:vars]
ansible_port=8022

[webservers]
server1    ansible_user=ansible

[application]
server1
server2

[MyProject:children]
proxy
webservers
application
```

You can add variables at either a host level or group level within the inventory file - An example is shown against 'server1' and the 'proxy' group.

There are times when you would want to pull the inventory from a cloud provider, or from LDAP, or you would want the inventory list to be generated using some logic, rather than from a simple text-based inventory list. For such purposes, we can use a Dynamic Inventory, but that will be covered later.


#### Playbooks
Playbooks are a description of policies that you want to apply to your hosts.  They consist of a number of Plays, each listing the roles and the arguments that will run on your hosts so that Ansible can set the required state. They are written in YAML, and as with all YAML files, they should begin with an “---”, and end with a “...”.  YAML is extremely syntax sensitive, so it is always and idea to test your playbook before running them.  The example below opens a few firewall ports, and then installs Java followed by Tomcat.

```
---

 - hosts: proxy
   become: true

   roles:
   - role: firewall
     firewall_ports:
     - { port:  80, proto: tcp, state: enabled }
     - { port:  443, proto: tcp, state: enabled }
   - role: java
   - role: tomcat

...
```


#### Roles
Simply put, roles are a further level of abstraction that can be useful for organizing  playbooks. As you add more and more functionality and flexibility to your playbooks, they  can become unwieldy and difficult to maintain as a single file. Roles allow you to create very minimal playbooks that then look to a directory structure to determine the actual
configuration steps they need to perform.

Organizing things into roles also allows you to reuse common configuration steps between different types of servers. This is already possible by "including" other files within a playbook, but with roles, these types of links between files are automatic based on a specific directory hierarchy.

In general, the idea behind roles is to allow you to define what a server is supposed to do, instead of having to specify the exact steps needed to get a server to act a certain way.

Roles are formatted in a specific way, shown below.

```
firewall/
├── defaults
│   └── main.yml
├── files
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── tasks
│   ├── redhat.yml
│   ├── ubuntu.yml
│   └── main.yml
└── templates
 └── foobar.conf.j2
 ```

Boilerplate roles can be created by using the ansible-galaxy command like below, which will create a new role called firewall.

```
ansible-galaxy init firewall
```


#### Tasks
This is the main entry-point into each Role, or specifically its
the first task within the main.yml file.  There can be more than one
yaml file, but the others will all be called from the main.yml.  An
example is shown below.

```
---

 - name: Unarchive maven
   unarchive:
     src: "{{ download_url }}"
     dest: "{{ maven_home_parent_directory }}"
     copy: no

 - name: Add /etc/profile.d/maven.sh file
   template:
     src: templates/maven.sh.j2
     dest: /etc/profile.d/maven.sh
     owner: root
     group: root
     mode: '0644'

 - name: Create Jenkins Users .m2 folder
   file:
     path: "{{ jenkins_home_directory }}/.m2"
     state: directory
     owner: jenkins
     group: jenkins
     mode: 0775

 - name: Add settings.xml file to jenkins .m2
   template:
     src: templates/settings.xml.j2
     dest: "{{ jenkins_home_directory }}/.m2/settings.xml"
     owner: jenkins
     group: jenkins
     mode: 0644

...
```

Each task begins with a name, which is optional, but makes it much easier to  understand the log outputs later.  The next item is the module that you would  like to run, followed by the parameters that you'd like to pass to it.


#### Modules
Modules are the executable plugins that get the real job done. Generally these are written using the Python language, and there is a section later in this course, where you can create a very simple plugin for yourself.  Usually modules can take “key: value” arguments and run in customized way depending up on the arguments themselves. A module can be invoked from command line or can be included in an Ansible playbook. You have already run an Ansible module in the last section, to confirm that Ansible was installed and working.  In this command the module is called 'ping'

```
ansible localhost -m ping
```

A list of all commonly used modules can be found here -
https://docs.ansible.com/ansible/latest/modules/list_of_all_modules.html?highlight=modules
