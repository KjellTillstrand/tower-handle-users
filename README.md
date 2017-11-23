tower-handle-users
=========

This role calls the tower-cli to create organizations, teams, users etc. The idea is to let the individual teams to administer the tower user handling via source controlled own playbook. 

Requirements
------------

tower-cli must be installed and configured 


Role Variables
--------------

see example 

Dependencies
------------

N/A

Example Playbook
----------------

- hosts: all
  vars:
    organization: "Some ORG"
    organization_state: present
    organization_description: "Organisation description "
    verify_ssl: False  
    tower_team:
        name: "ExampleTeam1"
        description: "This is the best team in the world"
        organization: "{{ organization }}"
        state: present
        tower_users:
           - username: kjelleman2
           # password: password
           # email: jdoe@example.org
           # first_name: John
           # last_name: Doe
           # superuser: false
           # state: present
           - username: jtoe
           # password: password
           # email: jtoe@example.org
           # first_name: Jane
           # last_name: Toe
           # superuser: true
           # state: present
        tower_projects:
            - name: "Team1_playbooks"
              description: "The playbooks for team 1 scm "
              organization: "{{ organization }}"
              scm_type: git
              scm_branch: "master"
              scm_update_on_launch: true
              scm_url: "https://git.some.url"
              state: present
        tower_inventories:
            - name: "Linux servers example"
              description: "Team1 Linux Servers"
              organization:  "{{ organization }}"
              state: present
              tower_hosts:
                  - name: Server1
                    description: "Server1 "
                    state: present
                  - name: Server2
                    description: "Server2 "
                    state: present
            - name: "Linux servers example2"
              description: "Team1 Linux Servers"
              organization:  "{{ organization }}"
              state: present
              tower_hosts:
                  - name: Server1
                    description: "Server3"
                    state: present
                  - name: Server2
                    description: "Server4"
                    state: present
        tower_credentials:
            - tower_credential:
                 name: "foo_scm_credential"
                 organization: "{{ organization }}"
                 kind: "scm"
                 description: This is a git credential for project Foo
                 user: extktd
                 state: present
  roles:
  - role: tower-handle-users

License
-------

GNU GENERAL PUBLIC LICENSE Version 3

Author Information
------------------

Authored by Kjel Tillstrand
