This repo contains a an example ansible-playbook using inventory and roles

To execute

```ansible-playbook -i inventory/deck/inventory --private-key=...```


## Roles 

Here is a basic structure of an Ansible role:

```
rolename/
├── defaults/           # Default variables for the role
│   └── main.yml
├── vars/               # Other variables for the role
│   └── main.yml
├── tasks/              # Main list of tasks to be executed by the role
│   └── main.yml
├── files/              # Files that can be deployed via this role
├── templates/          # Templates with Jinja2 templating language
├── handlers/           # Handlers, which may be used by this role or even anywhere outside this role
│   └── main.yml
└── meta/               # Metadata for the role, including role dependencies
    └── main.yml
```

- **defaults**: Contains default variables for the role. These have the lowest precedence, making them easy to override.
- **vars**: Variables here are more difficult to override and are typically used for setting internal role variables that the user should not change.
- **tasks**: Contains the main list of tasks that the role will execute.
- **files**: Contains files that can be deployed with this role.
- **templates**: Contains templates that can use Ansible’s templating system to dynamically generate files based on variables.
- **handlers**: Contains handlers, which are tasks that respond to a "notify" directive and are usually used to handle services (e.g., restarting a service when a config file changes).
- **meta**: Contains metadata for the role, such as the author, support details, and dependencies on other roles.


## Group Vars

In Ansible, `group_vars` is a directory that can exist as a subdirectory of your Ansible inventory directory or alongside your playbook. It is used to set variables for groups of hosts in your inventory. This allows you to apply specific configurations to different groups of hosts without having to repeat the same information across multiple host entries in your inventory file.

Here's how `group_vars` works:

1. **Directory Structure**: Within your Ansible project directory, you can create a `group_vars` directory. Inside this directory, you can create files named after each of your inventory groups.

   For example, if you have an inventory group called `[webserver]`, you can create a file named `webserver.yml` inside the `group_vars` directory.

2. **Defining Variables**: Within each `group_vars` file, you define variables in YAML format. These variables will be automatically applied to all hosts that are part of the corresponding group when you run your playbooks.

   ```yaml
   # group_vars/webserver.yml
   http_port: 80
   max_clients: 200
   ```

3. **Using Variables**: When you run a playbook, Ansible automatically loads variables from the appropriate `group_vars` file based on the groups each host belongs to. You can then use these variables in your playbooks, roles, and templates.
