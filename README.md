# users

[![Build Status](https://drone.osshelp.ru/api/badges/ansible/users/status.svg)](https://drone.osshelp.ru/ansible/users)

The role for Ansible, which manages system users.

## Usage (example)

See [molecule playbook](molecule/default/playbook.yml).

## Available parameters

### Main

Here are required parameters.

| Param | Description |
| -------- | -------- |
| `users` | List of users |
| `users.[].name` | User name |

### Additional

Here are not mandatory parameters.

| Param | Description |
| -------- | -------- |
| `users.[].state` | `present` or `absent`. Default `present` |
| `users.[].comment` | Short user description |
| `users.[].create_home` | Create home dir. Default `yes` |
| `users.[].groups` | List of groups user will be added to (the main user group is not included) |
| `users.[].group` | Main user group. Default = user name. Shouldn't be edited |
| `users.[].home` | User home. Default `/home/user.name` |
| `users.[].password` | User password hash. Generation example bellow |
| `users.[].remove` | This only affects state=absent, it attempts to remove directories associated with the user |
| `users.[].shell` | User shell. Default `/bin/bash` |
| `users.[].system` | System user or not. Default `no` |
| `users.[].uid` | User uid. Works with user.gid only |
| `users.[].gid` | Main user group gid. Works with user.uid only |
| `users.[].rsa_key` | Public part of user rsa key |

## FAQ

### User password generation

``` shell
ansible all -i localhost, -m debug -a "msg={{ 'password_here' | password_hash('sha512') }}"
```

Put a password hash into secrets (e.g. ansible vault).

## Useful links

- [Ansible user module](https://docs.ansible.com/ansible/latest/modules/user_module.html)
- [Ansible encrypted password generation](https://docs.ansible.com/ansible/faq.html#how-do-i-generate-encrypted-passwords-for-the-user-module)
- [Ansible authorized_key module](https://docs.ansible.com/ansible/latest/modules/authorized_key_module.html)

## TODO

- rename variable rsa_key -> rsa_key_pub (or something with pub)
- multiple authorized_key pub keys
- homedir mode. default 755

## License

GPL3

## Author

OSSHelp Team, see <https://oss.help>
