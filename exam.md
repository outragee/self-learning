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
         
         
        #Создание физического тома.  Выполняется с помощью команды pvcreate с указанием диска  созданного на предыдущем шаге. Выполняется для каждого используемого устройства.
        
        [exam@centos2 ~]$ sudo pvcreate /dev/sdb1 
        Physical volume "/dev/sdb1" successfully created.
        [exam@centos2 ~]$ sudo pvcreate /dev/sdc1 
        Physical volume "/dev/sdc1" successfully created.
        [exam@centos2 ~]$ sudo pvs
        PV         VG     Fmt  Attr PSize    PFree   
        /dev/sda2  centos lvm2 a--    <4.00g       0 
        /dev/sdb1         lvm2 ---  1023.00m 1023.00m
        /dev/sdc1         lvm2 ---  1023.00m 1023.00m
        
        #Создание группы томов. Для создания пула из одного или нескольких физических устройств используется утилита vgcreate.        
        
        [exam@centos2 ~]$ sudo vgcreate exam /dev/sdb1
        Volume group "exam" successfully created
        [exam@centos2 ~]$ sudo vgcreate exam2 /dev/sdc1
        Volume group "exam2" successfully created
        [exam@centos2 ~]$ sudo vgdisplay
        --- Volume group ---
        VG Name               exam
        System ID             
        Format                lvm2
        Metadata Areas        1
        Metadata Sequence No  3
        VG Access             read/write
        VG Status             resizable
        MAX LV                0
        Cur LV                0
        Open LV               0
        Max PV                0
        Cur PV                1
        Act PV                1
        VG Size               1020.00 MiB
        PE Size               4.00 MiB
        Total PE              255
        Alloc PE / Size       0 / 0   
        Free  PE / Size       255 / 1020.00 MiB
        VG UUID               ZaCQfS-qOgy-JRkv-yY91-0zTU-Vkgr-oWLewu
   
        --- Volume group ---
        VG Name               exam2
        System ID             
        Format                lvm2
        Metadata Areas        1
        Metadata Sequence No  1
        VG Access             read/write
        VG Status             resizable
        MAX LV                0
        Cur LV                0
        Open LV               0
        Max PV                0
        Cur PV                1
        Act PV                1
        VG Size               1020.00 MiB
        PE Size               4.00 MiB
        Total PE              255
        Alloc PE / Size       0 / 0   
        Free  PE / Size       255 / 1020.00 MiB
        VG UUID               NVIQWL-Kay2-CASy-CkXL-7ePf-fBPH-FavHin



        #Создание логического тома в созданной группе томов. LVM предоставляет возможность использовать как все пространство созданной группы томов под один логический том, так и создать несколько логических томов.
        #Флаги -L (весь размер),  можно указать -l — в таком случае можно в качестве размера логического тома указывать количество  используемых экстентов или же указать размер в процентах от свободного пространств
        
        [exam@centos2 ~]$ sudo lvcreate -l +100%FREE -n logs_exam exam
        Logical volume "logs_exam" created.
        [exam@centos2 ~]$ sudo lvcreate -l +100%FREE -n logs2_exam exam2
        Logical volume "logs2_exam" created.
        [exam@centos2 ~]$ sudo lvs
        LV         VG     Attr       LSize    Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
        root       centos -wi-ao----   <3.50g                                                    
        swap       centos -wi-ao----  512.00m                                                    
        logs_exam  exam   -wi-a----- 1020.00m                                                    
        logs2_exam exam2  -wi-a----- 1020.00m       
        

        









