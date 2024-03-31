### OTUS-Linux-2023-10-L37 | LDAP  

В репозитории Vagrantfile и окружение ansible разворачивают LDAP-сервер на дистрибутиве FreeIPA, а также две клиентские машины.
После установки на сервере добавляется пользователь *otus-user*.  
Далее разворачиваются две клиентских ВМ в которых создаются уникальные пользователи (otus-user1 и otus-user2) и также добавляются на сервер с ключом ssh-rsa.

Список пользователей зарегистрированных на сервере:  

```
[root@ipa ~]# ipa user-find
---------------
4 users matched
---------------
  User login: admin
  Last name: Administrator
  Home directory: /home/admin
  Login shell: /bin/bash
  Principal alias: admin@OTUS.LAN, root@OTUS.LAN
  UID: 1260000000
  GID: 1260000000
  Account disabled: False

  User login: otus-user
  First name: Otus
  Last name: User
  Home directory: /home/otus-user
  Login shell: /bin/sh
  Principal name: otus-user@OTUS.LAN
  Principal alias: otus-user@OTUS.LAN
  Email address: otus-user@otus.lan
  UID: 1260000003
  GID: 1260000003
  Account disabled: False

  User login: otus-user1
  First name: Otus
  Last name: User1
  Home directory: /home/otus-user1
  Login shell: /bin/sh
  Principal name: otus-user1@OTUS.LAN
  Principal alias: otus-user1@OTUS.LAN
  Email address: otus-user1@otus.lan
  UID: 1260000004
  GID: 1260000004
  SSH public key fingerprint: SHA256:SzMGU+UNhBs0OGKebPaTr9NFX/2GMbs5BtllSgzddhQ otus-user1@client1.otus.lan (ssh-rsa)
  Account disabled: False

  User login: otus-user2
  First name: Otus
  Last name: User2
  Home directory: /home/otus-user2
  Login shell: /bin/sh
  Principal name: otus-user2@OTUS.LAN
  Principal alias: otus-user2@OTUS.LAN
  Email address: otus-user2@otus.lan
  UID: 1260000005
  GID: 1260000005
  SSH public key fingerprint: SHA256:8Lsx4+Vi7oZS+EGh2DGYlihNq/Jh97NHd7kC7icv6NU otus-user2@client2.otus.lan (ssh-rsa)
  Account disabled: False
----------------------------
Number of entries returned 4
----------------------------
```
Список хостов зарегистрированных на сервере:
```
[root@ipa ~]# ipa host-find
---------------
3 hosts matched
---------------
  Host name: client1.otus.lan
  Platform: x86_64
  Operating system: 4.18.0-532.el8.x86_64
  Principal name: host/client1.otus.lan@OTUS.LAN
  Principal alias: host/client1.otus.lan@OTUS.LAN
  SSH public key fingerprint: SHA256:wK8qMIJlWRA4dPZwxwbGP8yy06FSLJe8VOIpIKz6IoI (ssh-ed25519),
                              SHA256:oGosWM9KEBhgiRoQifMds0PL1u0JPTjMUKehsfFdvo0 (ecdsa-sha2-nistp256),
                              SHA256:8afAQQpaTisGX2m19bf/WeU0XXbslNag/fO8emba8jI (ssh-rsa)

  Host name: client2.otus.lan
  Platform: x86_64
  Operating system: 4.18.0-532.el8.x86_64
  Principal name: host/client2.otus.lan@OTUS.LAN
  Principal alias: host/client2.otus.lan@OTUS.LAN
  SSH public key fingerprint: SHA256:VbfX3T21kl1M3LKjMERUJLXi3l0IPKZMDohZGbG+me4 (ssh-ed25519),
                              SHA256:XyeAh9axEuo7QaWUrUirbGA2F65WLOr+K6dO4jKeUHo (ecdsa-sha2-nistp256),
                              SHA256:h2auRjaXcqm5t8Ksa3b3ShfGoYYIVTITuJTUKjyTZuA (ssh-rsa)

  Host name: ipa.otus.lan
  Principal name: host/ipa.otus.lan@OTUS.LAN
  Principal alias: host/ipa.otus.lan@OTUS.LAN
  SSH public key fingerprint: SHA256:28bX/ft7rOsGfp8rviyXeIlxpw+cqGQQ+u3EkZHTnXA (ecdsa-sha2-nistp256),
                              SHA256:AE7x2YDyNAwGKDAY52EdZGUUfu7MxB1tg+6MnKgbO4Q (ssh-ed25519),
                              SHA256:0KIVR79q2IXEKU+flEpQhFHZW2Q9DK7ibwNTsHTSopo (ssh-rsa)
----------------------------
Number of entries returned 3
----------------------------
[root@ipa ~]# 
```
