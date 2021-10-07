rsyslog
=========

Install and configure complex rsyslog configurations for both client and server deployments.

Requirements
------------

N/A

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

- hosts: syslog-server
  become: yes
  roles:
    - role: rsyslog
      vars:
        rsyslog_rulesets:
          relp_rulset:
          - outputs: [ remotefile ]
        rsyslog_inputs:
          relp_input:
            type: relp
            params:
              port: 2514
              address: "{{ ansible_default_ipv4.address }}"
              ruleset: relp_ruleset
        rsyslog_outputs:
          remotefile:
            type: file
            params:
              file: /var/log/remotefile
  tags: [ rsyslog, syslog_server ]

- hosts: all
  become: yes
  roles:
    - role: rsyslog
      rsyslog_outputs:
        relp_output:
          type: relp
          params:
            port: 2514
            address: syslog-server
  tags: [ syslog, syslog-client ]

License
-------

Apache-2

Author Information
------------------

N/A
