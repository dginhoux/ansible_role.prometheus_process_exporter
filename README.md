# ROLE dginhoux.prometheus_process_exporter



## DESCRIPTION

This ansible role install, configure and uninstall prometheus process exporter.<br />
It can be deploy as binary downloaded from github OR as docker (no public image, you have to build an image and push to a registry)



## REQUIREMENTS

#### SUPPORTED PLATFORMS

This role require a supported platform.<br />
It will skip process with unsupported platform to avoid any compatibility problem.<br />
This behaviour can be bypassed by settings the following variable `asserts_bypass=True`.

| Platform | Versions |
|----------|----------|
| Debian | buster, bullseye |
| Fedora | 33, 34, 35, 36, 37 |
| EL | 7, 8 |

#### ANSIBLE VERSION

Ansible >= 2.13

#### DEPENDENCIES

None.



## INSTALLATION

#### ANSIBLE GALAXY

```shell
ansible-galaxy install dginhoux.prometheus_process_exporter
```
#### GIT

```shell
git clone https://github.com/dginhoux/ansible_role.prometheus_process_exporter dginhoux.prometheus_process_exporter
```


## USAGE

#### EXAMPLE PLAYBOOK

```yaml
- hosts: all
  roles:
    - name: start role dginhoux.prometheus_process_exporter
      ansible.builtin.include_role:
        name: dginhoux.prometheus_process_exporter
```


## VARIABLES

#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml` : 

```yaml
deploy_process_exporter: install
deploy_process_exporter_mode: binary
prometheus_process_exporter_docker_image: ncabatoff/process-exporter
prometheus_process_exporter_name: process-exporter
prometheus_process_exporter_version: 0.7.10
prometheus_process_exporter_arch: amd64
prometheus_process_exporter_download_url: >-
  https://github.com/ncabatoff/process-exporter/releases/download/
  v{{prometheus_process_exporter_version}}/
  {{prometheus_process_exporter_name}}-{{prometheus_process_exporter_version}}.
  linux-{{prometheus_process_exporter_arch}}.tar.gz
prometheus_process_exporter_bin_path: /usr/local/bin/{{prometheus_process_exporter_name}}
prometheus_process_exporter_conf_file_path: /etc/process-explorer.yml
# prometheus_process_exporter_conf_file_content: ""
prometheus_process_exporter_conf_file_content: |
  process_names:
    - name: all
      cmdline: 
      - '.+'
prometheus_process_exporter_state: started
prometheus_process_exporter_enabled: true
prometheus_process_exporter_port: 9256
prometheus_process_exporter_run_user: process-exporter
prometheus_process_exporter_nice_level: 0
prometheus_process_exporter_options: >-
  -config.path {{ prometheus_process_exporter_conf_file_path }}
  -web.listen-address :{{ prometheus_process_exporter_port }}
  -web.telemetry-path /metrics
```

#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.

`NOT USED BY THIS ROLE`



## AUTHOR

Dany GINHOUX - https://github.com/dginhoux



## LICENSE

MIT
