# Ansible
In Ansible, organizing files and folders effectively is key for maintaining clarity and efficiency in your automation projects. Here’s a common structure for Ansible projects:

### Typical Ansible Directory Structure

```
my_ansible_project/
├── ansible.cfg
├── inventory/
│   └── hosts
├── roles/
│   ├── common/
│   │   ├── tasks/
│   │   ├── handlers/
│   │   ├── templates/
│   │   ├── files/
│   │   └── defaults/
│   └── webserver/
│       ├── tasks/
│       ├── handlers/
│       ├── templates/
│       ├── files/
│       └── defaults/
├── playbooks/
│   └── site.yml
├── group_vars/
│   └── all.yml
└── host_vars/
    └── myhost.yml
```

### Description of Each Directory/File

- **`ansible.cfg`**: Configuration file for Ansible, where you can set various settings and paths for your project.
- **`inventory/`**: Contains your inventory files. The `hosts` file typically lists your managed nodes and their groupings.
- **`roles/`**: Contains roles which are reusable units of configuration. Each role has its own directory with subdirectories like:
  - **`tasks/`**: Contains task files.
  - **`handlers/`**: Contains handler files (for actions triggered by tasks).
  - **`templates/`**: Contains Jinja2 templates.
  - **`files/`**: Contains static files to be copied to remote hosts.
  - **`defaults/`**: Contains default variables for the role.
- **`playbooks/`**: Contains playbooks that define what should be done on the hosts. The `site.yml` file is usually the entry point for running playbooks.
- **`group_vars/`**: Contains variables specific to groups of hosts.
- **`host_vars/`**: Contains variables specific to individual hosts.

### Example Files

- **`inventory/hosts`**:
  ```ini
  [webservers]
  web1.example.com
  web2.example.com

  [dbservers]
  db1.example.com
  ```

- **`playbooks/site.yml`**:
  ```yaml
  - hosts: webservers
    roles:
      - webserver

  - hosts: dbservers
    roles:
      - common
  ```

- **`roles/webserver/tasks/main.yml`**:
  ```yaml
  - name: Install nginx
    apt:
      name: nginx
      state: present
  ```

This structure can be adapted based on the complexity and needs of your project, but this layout is a good starting point for most Ansible projects.
