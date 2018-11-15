# proxysql_proxysql_servers

Adds or removes ProxySQL hosts using the ProxySQL admin interface.

## Install

To use the `proxysql_proxysql_servers` module just copy the file into
`./library`, alongside your top level playbooks, or copy it into the path
specified by `ANSIBLE_LIBRARY` or the `--module-path` command line option.

## Options

| parameter         | required | default   | choices                                  | comments                                                                        |
| ----------------- | -------- | --------- | ---------------------------------------- | ------------------------------------------------------------------------------- |
| comment           | no       |           |                                          | Text field that can be used for any purposed defined by the user.               |
| config_file       | no       |           |                                          | Specify a config file from which login_user and login_password are to be read.  |
| hostname          | yes      |           |                                          | The ip address at which the ProxySQL instance can be contacted.                 |
| load_to_runtime   | no       | True      |                                          | Dynamically load mysql host config to runtime memory.                           |
| login_host        | no       | 127.0.0.1 |                                          | The host used to connect to ProxySQL admin interface.                           |
| login_password    | no       | None      |                                          | The password used to authenticate to ProxySQL admin interface.                  |
| login_port        | no       | 6032      |                                          | The port used to connect to ProxySQL admin interface.                           |
| login_user        | no       | None      |                                          | The username used to authenticate to ProxySQL admin interface.                  |
| login_unix_socket | no       |           |                                          | The unix socket to communicate to the ProxySQL admin interface.                 |
| port              | no       | 6032      |                                          | The port at which the ProxySQL instance can be contacted.                       |
| save_to_disk      | no       | True      |                                          | Save ProxySQL servers config to sqlite db on disk to persist the configuration. |
| state             | no       | present   | <ul><li>present</li><li>absent</li></ul> | When C(present) - adds the host, when C(absent) - removes the host.             |
| weight            | no       | 0         |                                          | Currently unused, but in the roadmap for future enhancements.                   |

## Examples

```yaml
# This example adds a server, it saves the ProxySQL server config to disk, but
# avoids loading the ProxySQL server config to runtime (this might be because
# several servers are being added and the user wants to push the config to
# runtime in a single batch using the M(proxysql_manage_config) module). It
# uses supplied credentials to connect to the ProxySQL admin interface.

- proxysql_proxysql_servers:
    login_user: admin
    login_password: admin
    hostname: mysql01
    state: present
    load_to_runtime: False

# This example removes a server, saves the ProxySQL server config to disk, and
# dynamically loads the ProxySQL server config to runtime. It uses credentials
# in a supplied config file to connect to the ProxySQL admin interface.

- proxysql_proxysql_servers:
    config_file: '~/proxysql.cnf'
    hostname: mysql02
    state: absent
```

## Dependencies

- [Ansible >= 2.7.1](https://github.com/ansible/ansible/releases/tag/v2.7.1)
- [PyMySQL](https://github.com/PyMySQL/PyMySQL)

## License

GNU General Public License v3.0+ (see
[https://www.gnu.org/licenses/gpl-3.0.txt](https://www.gnu.org/licenses/gpl-3.0.txt))

## Author Information

- Based on the [proxysql_backend_servers](https://github.com/ansible/ansible/blob/devel/lib/ansible/modules/database/proxysql/proxysql_backend_servers.py) module from the Ansible core
- Timo Runge
