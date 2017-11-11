# Example

This role will enable your pub key in order to access via only certificates and not via password disabling it.

If you do not have any certificate, please generate one like the example:
```bash
$ ssh-keygen -t rsa -b 4096 -C "user_test@example.org"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/someone/.ssh/id_rsa): user_test
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in user_test.
Your public key has been saved in user_test.pub.
The key fingerprint is:
SHA256:DUHuGMXpbcjjYhRf1bDk+/wW4uOELH9CDdpchziahLI user_test@example.org
The key's randomart image is:
+---[RSA 4096]----+
|       o+. .+o   |
|      .oo..o ..  |
|      .=++  + .  |
|     ..=*+o+ + . |
|     .+.SoB * .  |
|     Eo .+.+.= . |
|     . . ..o..+ .|
|          o..+ ..|
|           .+....|
+----[SHA256]-----+
```

Then you can continue setting the vars, in our example:
```yaml
# maintenance.yml
---
- name: Playbook for setup vagrant server
  hosts: all
  become: True

  vars:
    - debug: yes
    - user_name: user_test
    - user_group: "{{ user_name }}"
    - user_home: "/home/{{ user_name }}"
    - user_ssh_pub_file: "./files/{{ user_name }}.pub"

  roles:
    - { role: xfornesa.vps-maintenance }
```

Then start the vagrant machine, install the requirements (roles required) and play the playbook as follows:
```bash
$ cd example
$ vagrant up
$ ansible-galaxy install --roles-path ./roles/ -r requirements.yml
$ sh setup.sh
$ sh maintenance.sh
```

After the setup, you can login via ssh:
```bash
$ chmod 600 ./files/user_test
$ ssh -i ./files/user_test user_test@localhost -p2230
