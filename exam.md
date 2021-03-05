**1.**
Первым шагом поднимем 2 виртуалки, предварительно добавив им еще по 2 диска .

**2.**
Добавим пользователя exam и разрешим ему sudo без пароля:
    
    sudo useradd -G adm,wheel -s /bin/bash exam
    sudo visudo 
        exam ALL=(ALL) NOPASSWD:ALL
    sudo passwd exam
    su - exam
    
**3.**
Создадим группу hadoop c GID 1111 ,  добавим пользователей и отметим что основная группа 1111, для каждого пользователя создадим домашнюю директорию,поместим пользователей в группу hadoop.
    
    [exam@centos2 ~]$ sudo useradd -m -G hadoop -g 1111 hadoop
    [exam@centos2 ~]$ sudo useradd -m -G hadoop -g 1111 yarn
    [exam@centos2 ~]$ sudo useradd -m -G hadoop -g 1111 hdfs

    
    
    [exam@centos2 ~]$ cat /etc/group
        hadoop:x:1111:hdfs,hadoop,hhdfs
    
    [exam@centos2 ~]$ sudo passwd hadoop  #сразу зададим пароль для пользователя hadoop 
    Changing password for user hadoop.
    New password: 
    Retype new password: 
    passwd: all authentication tokens updated successfully.

Настроим ssh между виртуальными машинами ,а также ssh из локальной машины в виртуальные.

    ssh-keygen #на виртуальных машинах (от пользователя hadoop).
    [hadoop@centos2 ~]$ ssh-keygen 
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/hadoop/.ssh/id_rsa): 
    Created directory '/home/hadoop/.ssh'.
    Enter passphrase (empty for no passphrase): 
    Enter same passphrase again: 
    Your identification has been saved in /home/hadoop/.ssh/id_rsa.
    Your public key has been saved in /home/hadoop/.ssh/id_rsa.pub.
    The key fingerprint is:
    SHA256:KlosT+pyrBtHbyOUMUUblnNwDFdIhppdNb8FXmC5tpM hadoop@centos2
    The key's randomart image is:
    +---[RSA 2048]----+
    |   .BB=++ +o.    |
    |   o+*=  =.o     |
    |  o+.+    o..    |
    |  o+.     oo     |
    |  +     S..o     |
    | o o   .  E      |
    |..+ O .    .     |
    |.ooX o           |
    |o*+ .            |
    +----[SHA256]-----+
 


    ssh-copy-id -i centos2@192.168.43.103
    ssh-copy-id -i centos1@192.168.43.249
    
    
