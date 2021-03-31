# sysctl

[![Build Status](https://drone.osshelp.ru/api/badges/ansible/sysctl/status.svg)](https://drone.osshelp.ru/ansible/sysctl)

Simple Ansible role which setups sysctl parameters.

## Usage (example)

### Default sysctl params only

```yaml
    - role: sysctl
```

### Custom sysctl params or override defaults

```yaml
    - role: sysctl
      sysctl_params:
        net.ipv4.ip_local_port_range: 10245 65535
        vm.overcommit_memory: 1
```

- `net.ipv4.ip_local_port_range: 10245 65535`. override default value "10240 65535"
- `vm.overcommit_memory: 1`. custom value.

## Available parameters

Role has only one parameter `sysctl_params`.

| Param | Description |
| -------- | -------- |
| `sysctl_params` | Key:Value dictionary |

- key = sysctl key name
- value = sysctl key value

### Default parameters

The role has list of default (typical) sysctl parameters in file [defaults/main.yml](defaults/main.yml):

- `sysctl_default_common_params`. Common params for host system or lxc container
- `sysctl_default_host_params`. Paras for host system + **sysctl_default_common_params**
- `sysctl_default_lxc_params`. Paras for lxc container + **sysctl_default_common_params**

## FAQ

### I am getting errors when applying a role

You should check the problematic parameters on the server. If any problematic parameters were removed in the new version of the role, then when applied to the server, the parameters added by the previous version of the role will not be removed. You need to delete it manually. This is a feature of the Ansible [sysctl module](https://docs.ansible.com/ansible/2.8/modules/sysctl_module.html).

## Useful links

- [Official documentation](https://linux.die.net/man/5/sysctl.conf)
- [Our article](https://oss.help/kb654)

## TODO

- check and add `ignoreerrors` parameter for [sysctl module](https://docs.ansible.com/ansible/latest/modules/sysctl_module.html) (scenarios when we can't apply the parameters right away)

## License

GPL3

## Author

OSSHelp Team, see <https://oss.help>
