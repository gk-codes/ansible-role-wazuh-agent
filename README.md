Ansible Role: Wazuh Agent
=========

This role deploys the Wazuh Agent to Linux servers.

Requirements
------------

Wazuh Server to connect the Agent to.

Role Variables
--------------

Available variables are listed below, along with default values (see defaults/main.yml):

`wazuh_agent_groups` corresponds to the Agent groups you have defined in your Wazuh environment. It is a comma-separated string, e.g. `'default,linux,debian'`.

`wazuh_agent_manager_url` is the FQDN or IP address of the Wazuh Manager you want the agent to connect to.

```yml
wazuh_agent_configuration_directory: /var/ossec
wazuh_agent_groups: 'default'
wazuh_agent_manager_url: 192.168.1.251
```

You can control whether you want to install or uninstall the Wazuh Agent. By default, it is installed. To uninstall, set 

- `wazuh_agent_service_state` to `stopped`
- `wazuh_agent_service_enabled` to `no`
- `wazuh_agent_package_state` to `absent`

The `wazuh_agent_configuration_directory` is removed in case you decide to uninstall the agent.

The `wazuh_agent_package_checksum`, `wazuh_agent_package_name` and `wazuh_agent_package_url` depend on the operating system the agent is installed on. You can tune the URL and corresponding checksum to your preferences.

```yml
wazuh_agent_package_checksum: sha256:fa507dee71ee4599b2393420f6d43a7e978f559e6db8987f3ad817ed2924532e
wazuh_agent_package_name: wazuh-agent.rpm
wazuh_agent_package_state: present
wazuh_agent_package_url: https://packages.wazuh.com/4.x/yum/wazuh-agent-4.5.2-1.x86_64.rpm
```

```yml
wazuh_agent_service_enabled: yes
wazuh_agent_service_name: wazuh-agent
wazuh_agent_service_state: started
```

Dependencies
------------

None.

Example Playbook
----------------

```yml

- name: Deploy the Wazuh Agent on Linux Servers.
  hosts: linux_servers
  become: yes
  become_method: sudo
  vars:
    wazuh_agent_service_state: started
    wazuh_agent_service_enabled: yes
    wazuh_agent_package_state: present
    wazuh_agent_manager_url: 192.168.1.251
    wazuh_agent_groups: 'default,linux,debian'

  roles:
    - gk.wazuh-agent

```

License
-------

MIT / BSD

Author Information
------------------

This role was created in 2023 by gk-codes.
