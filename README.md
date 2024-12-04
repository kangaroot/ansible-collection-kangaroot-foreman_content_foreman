# Ansible collection: kangaroot.foreman_content_foreman

Collection for configuring Foreman repositories in a Foreman/Katello installation.

The Foreman repositories that can be configured from this collection are:

- Foreman 3.10:
  - EL7:
    - Foreman Client 3.10[^3]
  - EL8[^2]:
    - Foreman 3.10
    - Foreman Plugins 3.10
    - Katello 4.12
    - Candlepin 4.3
    - Pulpcore 3.16
    - Puppet 7
    - Foreman Client 3.10[^3]
  - EL9:
    - Foreman 3.10
    - Foreman Plugins 3.10
    - Katello 4.12
    - Candlepin 4.3
    - Pulpcore 3.16
    - Puppet 7
    - Foreman Client 3.10[^3]

- Foreman 3.11:
  - EL7:
    - Foreman Client 3.11[^3]
  - EL8[^2]:
    - Foreman 3.11
    - Foreman Plugins 3.11
    - Katello 4.13
    - Candlepin 4.3
    - Pulpcore 3.49
    - Puppet 7
    - Foreman Client 3.11[^3]
  - EL9:
    - Foreman 3.11
    - Foreman Plugins 3.11
    - Katello 4.13
    - Candlepin 4.4
    - Pulpcore 3.49
    - Puppet 7
    - Foreman Client 3.11[^3]

- Foreman 3.12[^1]:
  - EL7:
    - Foreman Client 3.12[^3]
  - EL8[^2]:
    - Foreman 3.12
    - Foreman Plugins 3.12
    - Katello 4.14
    - Candlepin 4.4
    - Pulpcore 3.49
    - Puppet 7
    - Foreman Client 3.12[^3]
  - EL9:
    - Foreman 3.12
    - Foreman Plugins 3.12
    - Katello 4.14
    - Candlepin 4.4
    - Pulpcore 3.49
    - Puppet 7
    - Foreman Client 3.12[^3]

[^1]: Enabled by default when enabling Foreman repositories.
[^2]: Enabled by default when enabling a specific Foreman release repository.
[^3]: Enabled by default when enabling a specific Foreman release and/or OS related repository.

## Requirements and Dependencies

Ansible Core 2.13.0 or higher is required for the roles in the collection.

The roles in this collection must be imported by the `kangaroot.foreman` collection. It is possible to directly use the roles in this collection but not recommended.

The `kangaroot.foreman` collection requires the `theforeman.foreman` and `theforeman.operations` collections. To install the required collections, execute:

```shell
ansible-galaxy collection install -r requirements.yml
```

in the collection directory.

## Collection Variables

The `group_vars` directory contains example vars files for the important variables used in the collection roles.

## Usage

The variable `foreman_content_roles` from the `foreman` role in the `kangaroot.foreman` collection contains a list content roles to import.

Add this collection content role to the `foreman_content_roles` list of content roles to import in your playbook project variables.

For example, add the `foreman_content_roles` variable in your `group_vars/foreman.yml` file of your playbook project:

```yaml
# Foreman content roles to include
foreman_content_roles:
  # Package only content
  - kangaroot.foreman_content_foreman.foreman_content_foreman
  - ...

  # OS content
  - kangaroot.foreman_content_rocky.foreman_content_rocky
  - ...

  # Builtin content
  - kangaroot.foreman_content_builtin.foreman_content_builtin
```

Also ensure that the Foreman repositories are enabled and at least one of the available Foreman release and/or OS related repositories is enabled as well by setting the appropriate enable variables:

```yaml
foreman_enable_foreman: true
foreman_enable_foreman312: true
foreman_enable_foreman312_el8: false
foreman_enable_foreman312_el9: true
foreman_enable_foreman312_el7_client: false
```

In your playbook, add a task to execute the `kangaroot.foreman.foreman` role:

```yaml
- name: Run kangaroot.foreman roles
  hosts: foreman
  roles:
    - kangaroot.foreman.foreman
```

