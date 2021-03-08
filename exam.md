**1.**
Первым шагом поднимем 2 виртуалки, предварительно добавив им еще по 2 диска .

**2.**
Добавим пользователя exam и разрешим ему sudo без пароля,также добавим его в 2 группы - администратов и группу wheel (из которой можно переходить в root ):
    
    sudo useradd -G adm,wheel -s /bin/bash exam
    sudo visudo 
        exam ALL=(ALL) NOPASSWD:ALL
    sudo passwd exam
    su - exam
    
**3.**
Создадим группу hadoop c GID 1111 ,  добавим пользователей и отметим что основная группа 1111, для каждого пользователя создадим домашнюю директорию,поместим пользователей в группу hadoop.
    
    [exam@centos2 ~]$ sudo groupadd -g 1111 hadoop 
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
 


    ssh-copy-id -i hadoop@192.168.0.17
    ssh-copy-id -i hadoop@192.168.0.18
    
    #Редактируем /etc/hosts
    [exam@centos2 ~]$ sudo vim /etc/hosts
    192.168.0.17 exam.vm1 exam1 #на vm2
    193.168.0.18 exam.vm2 exam2 #на vm1

    
***5.*** 
Установим OpenJDK8 из репозитория CentOS. Скачаем архив по ссылке (тут есть несколько вариантов , самый простой это установить wget а затем пройти по ссылке в задании и скопировать ссылку на кнопке download tar.gz). Второй вариант ,скачать на локальную машину и загрузить через scp на виртуальные. Затем разархивируем файлы в директорию /opt/hadoop-3.1.2/ и сделаем симлинк.

        
        [exam@centos2 ~]$ sudo yum install java-1.8.0-openjdk
        [exam@centos2 ~]$ sudo yum install wget
        [exam@centos2 ~]$ wget https://archive.apache.org/dist/hadoop/common/hadoop-3.1.2/hadoop-3.1.2.tar.gz
        [exam@centos2 ~]$ ls
        hadoop-3.1.2.tar.gz
        [exam@centos2 ~]$ sudo tar xf hadoop-3.1.2.tar.gz -C /opt/
        [exam@centos2 local]$ ln -s /opt/hadoop-3.1.2/ /usr/local/hadoop/current

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
        

        
        
        #Форматируем разделы LV в ext4 , создаем директории и смонтируем в них разделы. 
        
        
        [exam@centos1 dev]$ sudo mkfs.ext4 /dev/mapper/exam-logs_exam 
        mke2fs 1.42.9 (28-Dec-2013)
        Filesystem label=
        OS type: Linux
        Block size=4096 (log=2)
        Fragment size=4096 (log=2)
        Stride=0 blocks, Stripe width=0 blocks
        65280 inodes, 261120 blocks
        13056 blocks (5.00%) reserved for the super user
        First data block=0
        Maximum filesystem blocks=268435456
        8 block groups
        32768 blocks per group, 32768 fragments per group
        8160 inodes per group
        Superblock backups stored on blocks: 
    	32768, 98304, 163840, 229376

        Allocating group tables: done                            
        Writing inode tables: done                            
        Creating journal (4096 blocks): done
        Writing superblocks and filesystem accounting information: done

        
        [exam@centos1 dev]$ sudo mkfs.ext4 /dev/mapper/exam2-logs2_exam 
        mke2fs 1.42.9 (28-Dec-2013)
        Filesystem label=
        OS type: Linux
        Block size=4096 (log=2)
        Fragment size=4096 (log=2)
        Stride=0 blocks, Stripe width=0 blocks
        65280 inodes, 261120 blocks
        13056 blocks (5.00%) reserved for the super user
        First data block=0
        Maximum filesystem blocks=268435456
        8 block groups
        32768 blocks per group, 32768 fragments per group
        8160 inodes per group
        Superblock backups stored on blocks: 
    	32768, 98304, 163840, 229376

        Allocating group tables: done                            
        Writing inode tables: done                            
        Creating journal (4096 blocks): done
        Writing superblocks and filesystem accounting information: done

        #Проверим что все верно:

        [exam@centos1 dev]$ lsblk
        NAME                 MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
        sda                    8:0    0    5G  0 disk 
        ├─sda1                 8:1    0    1G  0 part /boot
        └─sda2                 8:2    0    4G  0 part 
          ├─centos-root      253:0    0  3.5G  0 lvm  /
          └─centos-swap      253:1    0  512M  0 lvm  [SWAP]
        sdb                    8:16   0    1G  0 disk 
        └─sdb1                 8:17   0 1023M  0 part 
          └─exam-logs_exam   253:2    0 1020M  0 lvm  
        sdc                    8:32   0    1G  0 disk 
        └─sdc1                 8:33   0 1022M  0 part 
          └─exam2-logs2_exam 253:3    0 1020M  0 lvm  
        sr0                   11:0    1 1024M  0 rom 


        [exam@centos1 ~]$ sudo mkdir /opt/mount1
        [exam@centos1 ~]$ sudo mkdir /opt/mount2
        [exam@centos1 dev]$ sudo mount /dev/mapper/exam-logs_exam /opt/mount1
        [exam@centos1 dev]$ sudo mount /dev/mapper/exam2-logs2_exam /opt/mount2       
        [exam@centos2 ~]$ sudo blkid
        [exam@centos1 dev]$ sudo blkid
        /dev/sda1: UUID="9ec108c8-7154-4fc5-a13d-e5b509e32f4d" TYPE="xfs" 
        /dev/sda2: UUID="J6cSmn-ngeI-WcLE-HNfk-lX5U-Sr9d-XOo45W" TYPE="LVM2_member" 
        /dev/mapper/centos-root: UUID="feba96e3-b375-4be6-8a1c-fdb05f2f36ef" TYPE="xfs" 
        /dev/mapper/centos-swap: UUID="0c74c958-d8a8-46f2-a8fd-ef78dbafbabd" TYPE="swap" 
        /dev/sdb1: UUID="bK60B6-lKN6-TbWl-QN1L-7daX-sDyp-lvoXTS" TYPE="LVM2_member" PARTUUID="363ef016-d1c9-45cd-aa99-125fabe40bd3" 
        /dev/sdc1: UUID="gSQGfW-5Deq-CBpG-lIqn-GAMA-efDl-jdNaVD" TYPE="LVM2_member" PARTLABEL="primary" PARTUUID="9f628ac0-d0a2-4c43-9755-7d174f1e7046" 
        /dev/mapper/exam-logs_exam: UUID="15542d95-bd14-400e-889f-30ffd740b13c" TYPE="ext4" 
        /dev/mapper/exam2-logs2_exam: UUID="fe8d5067-e4fb-4b68-8f19-9c086bd1ecbb" TYPE="ext4" 
        
        #Чтобы автоматически монтировать  файловую систему после перезагрузки, добавим запись в /etc/fstab
        UUID=15542d95-bd14-400e-889f-30ffd740b13c /opt/mount1 ext4 default 0 0
        Первое поле (UUID=…) – идентификатор раздела, который можно посмотреть утилитой blkid.

        Второе (/opt/mount1) – точка монтирования раздела

        Третье (ext4) – тип файловой системы

        Четвертое  (defaults) — опции монтировании в fstab. Опция defaults — использование параметров по-умолчанию: exec, auto, rw, nouser, async, nosuid, atime.         Разрешить запуск исполняемых файлов,  установить права на чтение и запись, обычным пользователям запретить подключать/отключать устройство, включение опции асинхронного ввода/вывода,  производить запись времени последнего доступа к файлу,  заблокировать работу SUID и SGID битов для устройства.

        Пятое поле — необходимость создавать резервные копии раздела утилите dump.
        0 – не создавать резервные копии.
        1 – разрешить резервные копии.

        Шестое — необходимость проверки файловой системы утилитой fsck

        0 – раздел не будет проверяться.
        1 –будет проверяться в первую очередь.
        2 –будет проверяться после раздела со значением 1.

        
        [exam@centos2 ~]$ sudo vim /etc/fstab    
       
        #
        # /etc/fstab
        # Created by anaconda on Mon Mar  8 13:35:43 2021
        #
        # Accessible filesystems, by reference, are maintained under '/dev/disk'
        # See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
        #
        /dev/mapper/centos-root /                       xfs     defaults        0 0
        UUID=9ec108c8-7154-4fc5-a13d-e5b509e32f4d /boot                   xfs     defaults        0 0
        /dev/mapper/centos-swap swap                    swap    defaults        0 0
        UUID=15542d95-bd14-400e-889f-30ffd740b13c /opt/mount1 ext4 defaults 0 0
        UUID=fe8d5067-e4fb-4b68-8f19-9c086bd1ecbb /opt/mount2 ext4 defaults 0 0

        
**7.**
Настройка директорий.


Для VM1:

        [exam@centos1 mount1]$ sudo mkdir namenode-dir
        [exam@centos1 mount1]$ sudo mkdir /opt/mount2/namenode-dir
        [exam@centos1 mount1]$ sudo chown hdfs:hadoop /opt/mount1/namenode-dir/
        [exam@centos1 mount1]$ sudo chown hdfs:hadoop /opt/mount2/namenode-dir/
        
        
Для VM2:

        [exam@centos2 mount1]$ sudo mkdir datanode-dir
        [exam@centos2 mount1]$ sudo mkdir /opt/mount2/datanode-dir
        [exam@centos2 mount1]$ sudo chown hdfs:hadoop /opt/mount1/datanode-dir/
        [exam@centos2 mount1]$ sudo chown hdfs:hadoop /opt/mount2/datanode-dir/


Для VM1 и VM2:


        [exam@centos1 mount1]$ sudo mkdir nodemanager-local-dir
        [exam@centos1 mount1]$ sudo mkdir /opt/mount2/nodemanager-local-dir
        [exam@centos1 mount1]$ sudo mkdir nodemanager-log-dir
        [exam@centos1 mount1]$ sudo mkdir /opt/mount2/nodemanager-log-dir
        [exam@centos2 mount1]$ sudo chown yarn:hadoop /opt/mount2/nodemanager-local-dir/
        [exam@centos2 mount1]$ sudo chown yarn:hadoop /opt/mount1/nodemanager-local-dir/
        [exam@centos2 mount1]$ sudo chown yarn:hadoop /opt/mount2/nodemanager-log-dir/
        [exam@centos2 mount1]$ sudo chown yarn:hadoop /opt/mount1/nodemanager-log-dir/


***8.***
Скачивание,переименование , жуткий sed...
Убив час, сделал следующий конвеер . Он берет из вывода finde имя файла , передает в sed, sed показывает и старое и новое значение , а затем команда mv при помощи подстановки xargs переименовывает файл.

        [exam@centos2 hadoop]$ sudo wget -nv https://gist.github.com/rdaadr/2f42f248f02aeda18105805493bb0e9b 
        2021-03-07 09:12:09 URL:https://gist.github.com/rdaadr/2f42f248f02aeda18105805493bb0e9b [178810] -> "2f42f248f02aeda18105805493bb0e9b" [1]
        [exam@centos2 hadoop]$ sudo find /usr/local/hadoop/current/etc/hadoop/ . -name "[0-9]*" -o -name "ba*" | sed 'p;s/.*/hadoop-env.sh/g' | sudo xargs -n2 mv
        [exam@centos2 hadoop]$ sudo wget https://gist.github.com/rdaadr/64b9abd1700e15f04147ea48bc72b3c7
        --2021-03-07 09:17:01--  https://gist.github.com/rdaadr/64b9abd1700e15f04147ea48bc72b3c7
        [exam@centos2 hadoop]$ sudo find /usr/local/hadoop/current/etc/hadoop/ . -name "[0-9]*" -o -name "ba*" | sed 'p;s/.*/core-site.xml/g' | sudo xargs -n2 mv
        [exam@centos2 hadoop]$ sudo wget -nv https://gist.github.com/rdaadr/2bedf24fd2721bad276e416b57d63e38
        2021-03-07 09:19:52 URL:https://gist.github.com/rdaadr/2bedf24fd2721bad276e416b57d63e38 [64584] -> "2bedf24fd2721bad276e416b57d63e38" [1]
        [exam@centos2 hadoop]$ sudo find /usr/local/hadoop/current/etc/hadoop/ [exam[exam@centos2 hadoop]$ sudo find /usr/local/hadoop/current/etc/hadoop/ . -name         "[0-9]*" -o -name "ba*" | sed 'p;s/.*/hdfs-site.xml/g' | sudo xargs -n2 mv
        [exam@centos2 hadoop]$ sudo wget -nv https://gist.github.com/Stupnikov-NA/ba87c0072cd51aa85c9ee6334cc99158
        2021-03-07 09:21:57 URL:https://gist.github.com/Stupnikov-NA/ba87c0072cd51aa85c9ee6334cc99158 [68735] -> "ba87c0072cd51aa85c9ee6334cc99158" [1]
        [exam@centos2 hadoop]$ sudo find /usr/local/hadoop/current/etc/hadoop/ . -name "[0-9]*" -o -name "ba*" | sed 'p;s/.*/yarn-site.xml/g' | sudo xargs -n2 mv
        [exam@centos2 hadoop]$ ls
        core-site.xml  hadoop-env.sh  hdfs-site.xml  yarn-site.xml

        #Задаем необходимые значения переменных , редактируя файлы, согласно заданию .
        
        /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.282.b08-1.el7_9.x86_64/jre/bin/java  #путь к java-home
        
