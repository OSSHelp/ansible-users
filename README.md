# users

[![Build Status](https://drone.osshelp.ru/api/badges/ansible/users/status.svg)](https://drone.osshelp.ru/ansible/users)

The role for Ansible, which manages system users.

## Usage (example)

```yaml
    - role: users
      users:
        - name: ubuntu
          state: absent
          remove: yes
        - name: testuser1
          comment: 'minimal params testuser1'
        - name: testuser2
          comment: 'testuser2 with custom uid/gid'
          user_uid: 1005
          user_gid: 2008
        - name: testuser3
          comment: 'testuser3'
          password: '$6$.n/2wFSVaJygIbBk$36h5TZt2V7ZbgZzcdrRVaDQXmQ6ZBMBj8dEOw0LStwz.fjNOpSgz4k989VjBzKvJJ2EY3L6AwPN8BtQ.q7vCA/'
          ssh_keys:
            - 'ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDhlHctdsQ2640wQz7KIwQ86KCF1GbVRyEDr/GJEtqri7H4m8QtITrAjQRGlq4TK0lek+XivTIgT3uzAJEpP8Wiqr7ke1ZyDZdJw+5GYm4lG4hZs5kkT+AU88j21xZQ1ww4aNw7bXZBNU8Tk38sLbFllXEfCsbrVFMvT499pfTAgNJ8xRrahkLegsTJA+1PJxHwPnEI5IEzSxfu6ChjNrjGtl4tCsRTMWP7UdVfolBE4WLKqpqoa7C9xdmVFauwn8Ah5FepfdgQuXtvlkqPtWr/sEhNUEAAEfyDZ1We5SzW5dBBQWIPsJ8UZRNz/yNJorlTyoXdVYR919dHYluxbGPf testuser6'
            - 'ssh-rsa 111AB3NzaC1yc2EAAAADAQABAAABAQCs4f11f0XjmYxACW0+w8VxFSAcMzhQF5CTVUJY9AIJZiFvdZeGVy5/ZsaqY2wseTPqizhCol1hMR6c423TeYCXICgfjh6XFwbbC48fNm0EaGDaogize0YSHsGvgRhz/rnX5X3Lk8RWYaXp3+ScayVnduM4ZjG81eDR5fxwHqK01S7ZhjliGE15enacOxr1SP/SywaWU8OU0FzZG/32RkcWihKZF43pkm9ylJq+638qW5MKDz0X1Ji07m7X9fTjEIIUTYsbW4NHefHCfZI6iXFkKIGpMqewcHrWiSxJB2XZn76gCyqLUKoyJY9GpT3riX1Hzm8ouzNs6d6aowreBt+5 root@tester'
```

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
| `users.[].ssh_keys` | Public part of user ssh keys |

## FAQ

### User password generation

``` shell
ansible all -i localhost, -m debug -a "msg={{ 'password_here' | password_hash('sha512') }}"
```

Put a password hash into secrets (e.g. ansible vault).

## Useful links

- [Ansible user module](https://docs.ansible.com/ansible/latest/modules/user_module.html)
- [Ansible encrypted password generation](https://docs.ansible.com/ansible/faq.html#how-do-i-generate-encrypted-passwords-for-the-user-module)
- [Ansible authorized_key module](https://docs.ansible.com/ansible/2.9/modules/authorized_key_module.html)

## TODO

- rename variable rsa_key -> rsa_key_pub (or something with pub)
- homedir mode. default 755

## License

GPL3

## Author

OSSHelp Team, see <https://oss.help>
