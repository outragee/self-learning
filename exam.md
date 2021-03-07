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

***4.***
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
    
***5.*** 
Установим OpenJDK8 из репозитория CentOS. Скачаем архив по ссылке (тут есть несколько вариантов , самый простой это установить wget а затем пройти по ссылке в задании и скопировать ссылку на кнопке download tar.gz). Второй вариант ,скачать на локальную машину и загрузить через scp на виртуальные. Затем разархивируем файлы в директорию /opt/hadoop-3.1.2/ и сделаем симлинк.

        
        [exam@centos2 ~]$ sudo yum install java-1.8.0-openjdk
        [exam@centos2 ~]$ sudo yum install wget
        [exam@centos2 ~]$ wget https://archive.apache.org/dist/hadoop/common/hadoop-3.1.2/hadoop-3.1.2.tar.gz
        [exam@centos2 ~]$ ls
        hadoop-3.1.2.tar.gz
        [exam@centos2 ~]$ sudo tar xf hadoop-3.1.2.tar.gz -C /opt/
        [exam@centos2 local]$ ln -s /usr/local/hadoop/current /opt/hadoop-3.1.2/

***6.***
Настройка дисков.

        [exam@centos2 ~]$ sudo fdisk /dev/sdb #первый диск , n — создать новый раздел
                                                             p — тип раздела primary    
                                                             t — сменить тип раздела на «Linux LVM», тип раздела — LVM соответствует код 8e
                                                             w — записать изменения на диск
        [exam@centos2 ~]$ sudo fdisk /dev/sdc #второй диск , аналогично.
         
        Создание физического тома.  Выполняется с помощью команды pvcreate с указанием диска  созданного на предыдущем шаге. Выполняется для каждого используемого устройства.
        

        
