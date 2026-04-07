# Ansible Role: Jenkins ([Ludus](https://ludus.cloud))

An Ansible Role that installs [Jenkins](https://www.jenkins.io/) on Debian/Ubuntu hosts and optionally configures an admin user and plugins.

> [!WARNING]
> The default admin credentials are `admin:admin`. Change `ludus_jenkins_admin_password` for any non-ephemeral environment.

## Requirements

None. Java (OpenJDK 17) is installed automatically.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    # Port Jenkins will listen on
    ludus_jenkins_http_port: 8080

    # Java packages to install
    ludus_jenkins_java_packages:
      - fontconfig
      - openjdk-17-jre

    # Jenkins version (empty string = latest)
    ludus_jenkins_version: ""

    # Whether to skip the initial setup wizard
    ludus_jenkins_skip_setup_wizard: true

    # List of Jenkins plugins to install
    ludus_jenkins_plugins:
      - git
      - workflow-aggregator
      - configuration-as-code

    # Jenkins admin credentials (used when setup wizard is skipped)
    ludus_jenkins_admin_user: admin
    ludus_jenkins_admin_password: admin

    # Additional Java arguments for Jenkins
    ludus_jenkins_java_args: ""

    # Jenkins home directory
    ludus_jenkins_home: /var/lib/jenkins

## Dependencies

None.

## Example Playbook

```yaml
- hosts: jenkins_hosts
  roles:
    - Whispergate.ludus_jenkins_role
  vars:
    ludus_jenkins_http_port: 8080
    ludus_jenkins_admin_password: "changeme"
```

## Example Ludus Range Config

```yaml
ludus:
  - vm_name: "{{ range_id }}-jenkins"
    hostname: "{{ range_id }}-jenkins"
    template: debian-12-x64-server-template
    vlan: 10
    ip_last_octet: 20
    ram_gb: 4
    cpus: 2
    roles:
      - Whispergate.ludus_jenkins_role
    role_vars:
      ludus_jenkins_admin_password: "changeme"
      ludus_jenkins_plugins:
        - git
        - workflow-aggregator
        - configuration-as-code
        - pipeline-stage-view
```

## License

MIT

## Author Information

This role was created by [Whispergate](https://github.com/Whispergate), for [Ludus](https://ludus.cloud/).
