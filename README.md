### OTUS-Linux-2023-10-L37 | LDAP  

В репозитории Vagrantfile и окружение ansible разворачивают LDAP-сервер на дистрибутиве FreeIPA, а также две клиентские машины.
После становки на сервере добавляется пользователь *otus-user*  
Далее разворачиваются две клиентских ВМ.

Добавление нового пользователя на сервере:  

>[root@ipa ~]# ipa user-add otus-user1 --first=Otus --last=User --password
>Password: 
>Введите Password ещё раз для проверки: 
>-----------------------
>Added user "otus-user1"
>-----------------------
>  User login: otus-user1
>  First name: Otus
>  Last name: User
>  Full name: Otus User
>  Display name: Otus User
>  Initials: OU
>  Home directory: /home/otus-user1
>  GECOS: Otus User
>  Login shell: /bin/sh
>  Principal name: otus-user1@OTUS.LAN
>  Principal alias: otus-user1@OTUS.LAN
>  User password expiration: 20240331165802Z
>  Email address: otus-user1@otus.lan
>  UID: 1064800004
>  GID: 1064800004
>  Password: True
>  Member of groups: ipausers
>  Kerberos keys available: True
>[root@ipa ~]# 

Проверка на клиенте:

>[root@client2 ~]# kinit otus-user1
>Password for otus-user1@OTUS.LAN: 
>Password expired.  You must change it now.
>Enter new password: 
>Enter it again: 
>[root@client2 ~]#

При веровм логине просит сменить пароль.
