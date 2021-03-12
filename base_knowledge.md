## Задачи:

 <details><summary>  Задания лекций 1-2  </summary>
  
  0. установить вторую ВМ с доступом только до первой ВМ.
  Все команды выполняются от имени созданного во время инсталляции пользователя (не root).
  
  1. Внутри директории /usr/share/man (хранилище встроенной документации) находятся каталоги, разбитые по секциям разделов помощи (man1, man2, man3) и по языкам (es, fr, ru).
Используя команду ls, необходимо вывести на экран все файлы, которые расположены в секционных директориях ы и содержат слово "config" в имени. Одним вызовом ls найти все файлы, содержащие слово "system" в каталогах /usr/share/man/man1 и /usr/share/man/man7
  
  2. Самостоятельно изучить команду find, предназначенную для поиска файлов/папок по заданным условиям (man find, find --help).
Найти в директории /usr/share/man все файлы, которые содержат слово "help" в имени, найти там же все файлы, имя которых начинается на "conf".
Какие действия мы можем выполнить с файлами, найденными командой find (не запуская других команд)? Приведите любой пример с комментарием.
  
  3. При помощи команд head и tail, выведите последние 2 строки файла /etc/fstab и первые 7 строк файла /etc/yum.conf
Что произойдёт, если мы запросим больше строк, чем есть в файле? Попробуйте выполнить это на примере, используя команду wc (word cound) для подсчёта количества строк в файле.
  
  4. Создайте в домашней директории файлы file_name1.md, file_name2.md и file_name3.md. Используя {}, переименуйте:
file_name1.md в file_name1.textdoc
file_name2.md в file_name2
file_name3.md в file_name3.md.latest
file_name1.textdoc в file_name1.txt
  
  5. Перейдите в директорию /mnt. Напишите как можно больше различных вариантов команды cd, с помощью которых вы можете вернуться обратно в домашнюю директорию вашего пользователя. Различные относительные пути также считаются разными вариантами.
  
  6. Создайте одной командой в домашней директории 3 папки new, in-process, processed. При этом in-process должна содержать в себе еще 3 папки tread0, tread1, tread2.
Далее создайте 100 файлов формата data[[:digit:]][[:digit:]] в папке new
Скопируйте 34 файла в tread0 и по 33 в tread1 и tread2 соответственно. Выведете содержимое каталога in-process одной командой
После этого переместите все файлы из каталогов tread в processed одной командой. Выведете содержимое каталога in-process и processed опять же одной командой
Сравните количество файлов в каталогах new и processed при помощи изученных ранее команд, если они равны удалите файлы из new
** Сравнение количества и удаление сделано при помощи условия

  7. Получить разворачивание фигурных скобок для выражения. Согласно стандартному поведению bash, стандартного для CentOS 7, скобки в приведённом ниже выражении развёрнуты не будут. Необходимо найти способ получить ожидаемый вывод.
a=1; b=3
echo file{$a..$b}
Необходимо предоставить модицицированную команду, результатом которой является следующий вывод: 
file1 file2 file3


</details>
 <details><summary>  Задания лекций 3-4 (awk,sed,vim) </summary>


 You have log file 'access.log'. It is simple apache log. Format is remote-IP - - [DATE] "method query protocol" status-code send-bytes-from-server "from-where-did-user-came" "user agent" "x-forwarded-for-header"
Sample can be downloaded from 

http://www.almhuette-raith.at/apache-log/access.log    (~650 Mb)



Awk
* What is the most frequent browser (user agent)?
* Show number of requests per month for ip 193.106.31.130 (for example: Sep 2016 - 100500 reqs, Oct 2016 - 0 reqs, Nov 2016 - 2 reqs...)
* Show total amount of data which server has provided for each unique ip (i.e. 100500 bytes for 1.2.3.4; 9001 bytes for 5.4.3.2 and so on)


Sed
* Change all user agents to "lynx"
* Masquerade all ip addresses. For example, 1.2.3.4 becomes "ip1", 3.4.5.6 becomse "ip2" and so on. Rewrite file.
Extra (*)

• Show list of unique ips, who made more then 50 requests to the same url within 10 minutes (for example too many requests to "/")

Learn vim:

   vimtutor / vimtutor ru (in your linux terminal with vim installed)
   
   http://www.vimgenius.com/
   
   https://vimvalley.com/vim-movement-speed-challenge/
   
Vim videos


   https://www.youtube.com/watch?v=aHm36-na4-4
   
   https://www.youtube.com/watch?v=XA2WjJbmmoM
   https://github.com/outragee/epam-learning/blob/main/homework.md
   https://www.youtube.com/watch?v=_NUO4JEtkDw
   
   https://www.youtube.com/watch?v=NzD2UdQl5Gc
   
   https://www.youtube.com/watch?v=5r6yzFEXajQ
   
 
 </details>

 <details><summary> Задания лекций 5-6 (users, groups, file access) </summary>
 
 Task 1: Users and groups

Используйте команды: groupadd, useradd, passwd, chage и другие.
Создайте группу sales с GID 4000 и пользователей bob, alice, eve c основной группой sales. 
Измените пользователям пароли.
Все новые аккаунты должны обязательно менять свои пароли каждый 30 дней.
Новые аккаунты группы sales должны истечь по окончанию 90 дней срока, а bob должен изменять его пароль каждые 15 дней.

Дополнительно:
Заставьте пользователей сменить пароль после первого логина.

Предварительный шаг:
Исследуйте файл /etc/login.defs.
Исследуйте, как работает команда date и как её использовать совместно с chage.



Task 2: Controlling access to files with Linux file system permissions

Используйте команды: su, mkdir, chown, chmod и другие.
Создайте трёх пользователей glen, antony, lesly.
У вас должна быть директория /home/students, где эти три пользователя могут работать совместно с файлами.
Должен быть возможен только пользовательский и групповой доступ, создание и удаление файлов в /home/students. 
Файлы, созданные в этой директории, должны автоматически присваиваться группе студентов students.

Предварительный шаг:
Исследуйте, для чего нужны файлы .bashrc и .profile.



Task3: ACL

Детективное агентство Бейкер Стрит создает коллекцию совместного доступа для хранения файлов дел, в которых члены группы bakerstreet будут иметь права на чтение и запись.
Ведущий детектив, Шерлок Холмс, решил, что члены группы scotlandyard также должны иметь возможность читать и писать в общую директорию. Тем не менее, Холмс считает, что инспектор Джонс является достаточно растерянным, и поэтому он должен иметь доступ только для чтения. 
Миссис Хадсон только начала осваивать Linux и смогла создать общую директорию и скопировать туда несколько файлов. Но сейчас время чаепития, и она попросила вас закончить работу.

Ваша задача - завершить настройку директории общего доступа. 
Директория и всё её содержимое должно принадлежать группе bakerstreet, при этом файлы должны обновляться для чтения и записи для владельца и группы (bakerstreet). У других пользователей не должно быть никаких разрешений. 
Вам также необходимо предоставить доступы на чтение и запись для группы scotlandyard, за исключением Jones, который может только читать документы.
Убедитесь, что ваша настройка применима к существующим и будущим файлам. После установки всех разрешений в директории проверьте от каждого пользователя все его возможные доступы.

Используйте команды: touch, mkdir, chgrp, chmod, getfacl, setfacl и другие. 
Создайте общую директорию /shares/cases.
Создайте группу bakerstreet с пользователями holmes, watson.
Создайте группу scotlandyard с пользователями lestrade, gregson, jones.
Задайте всем пользователям безопасные пароли.

Предварительный шаг:
От суперпользователя создайте папку /share/cases и создайте внутри 2 файла murders.txt и moriarty.txt.
 
 </details>
 
 
 <details><summary>  Задания лекций 7-8 ( Process, systemd, cron/anacron, lsof ) </summary>
 
 Processes

1. Run a sleep command three times at different intervals
2. Send a SIGSTOP signal to all of them in three different ways.
3. Check their statuses with a job command
4. Terminate one of them. (Any)
5. To other send a SIGCONT in two different ways.
6. Kill one by PID and the second one by job ID

systemd
1. Write two daemons: one should be a simple daemon and do sleep 10 after a start and then do echo 1 > /tmp/homework, the second one should be oneshot and do echo 2 > /tmp/homework without any sleep
2. Make the second depended on the first one (should start only after the first)
3. Write a timer for the second one and configure it to run on 01.01.2019 at 00:00
4. Start all daemons and timer, check their statuses, timer list and /tmp/homework
5. Stop all daemons and timer

cron/anacron
1. Create an anacron job which executes a script with echo Hello > /opt/hello and runs every 2 days
2. Create a cron job which executes the same command (will be better to create a script for this) and runs it in 1 minute after system boot.
3. Restart your virtual machine and check previous job proper execution
-----

lsof
1. Run a sleep command, redirect stdout and stderr into two different files (both of them will be empty).
2. Find with the lsof command which files this process uses, also find out where it gets stdout from.
3. List all ESTABLISHED TCP connections ONLY with lsof

 </details>
 
 <details><summary>  Задания лекций 9-10 (SSH , timezone , logs )  </summary>
 
 
 **Task 1:**
 
 
 *As a result of each point, you should provide a corresponding command.localhost - your CentOS VM running in VirtualBoxremotehost - 40.68.74.188 (public IP)webserver - 10.0.0.5 (private IP)1.1. SSH to remotehost using username and password provided to you in Slack. Logout from remotehost.*
 
  1.2. Generate new SSH key-pair on your localhost with name "hw-5" (keys should becreated in ~/.ssh folder).
  
  1.3. Set up key-based authentication, so that you can SSH to  remotehost  withoutpassword.
  
  1.4. SSH to remotehost without password. Log out from remotehost.
  
  1.5. Create SSH config file, so that you can SSH to remotehost simply running`sshremotehost` command. As a result, provide output of command`cat ~/.ssh/config`.
  
  1.6. Using command line utility (curl or telnet) verify that there are some webserverrunning on port 80 of webserver.  Notice that webserver has a private network IP, soyou can access it only from the same network (when you are on remotehost that runsin the same private network). Log out from remotehost.
  
  1.7. Using SSH setup port forwarding, so that you can reach  webserver from yourlocalhost (choose any free local port you like).
  
  1.8 Like in 1.6, but on localhost using command line utility verify that localhost andport you have specified act like webserver, returning same result as in 1.6.
  
  1.9 (*) Open webserver webpage in browser of your Host machine of VirtualBox(Windows, or Mac, or whatever else you use). You may need to setup port forwardingin settings of VirtualBox.
 
 
 
**Task 2:**

*Following tasks should be executed on your localhost as you will need root privileges*

  2.1.Imagine your localhost has been relocated to Havana. Change the time zone onthe localhost to Havana and verify the time zone has been changed properly (may bemultiple commands).
  
  2.2. Find all systemd journal messages on localhost, that were recorded in the last 50minutes and originate from a system service started with user id 81 (single command).
  
  2.3. Configure  rsyslogd  by adding  a  rule  to  the  newly created  configuration   file/etc/rsyslog.d/auth-errors.conf to log all security and authentication messages with thepriority alert and higher to the  /var/log/auth-errors file. Test the newly added logdirective with the logger command (multiple commands).
 
 </details>
 
 
 <details><summary> Задание 11-12 ( Networking )  </summary>
 
**1.** С помощью утилиты nmcli добавте второй ip адрес сетевому интерфейсу enp0s3 (или тому, который является "основным" для вашей машины):
  
   1.1 IP Адрес должен быть назначен из пула немаршрутизируемых в Интернете пулов (aka серых IP)
   
   1.2 Адрес НЕ должен принадлежать пулу адресов, который уже назначен какому-либо из интерфейсов
   
   1.3 В подсети нового адреса должно быть как можно меньше адресов (broadcast и network адрес назначать интерфейсу нельзя)
   
   1.4 перезагрузите машину, убедитесь что оба интерфейса имеет оба адреса (вы должны мочь подключиться по ssh к новому ip адресу)
   

**2.** Новый IP адрес должен "резолвиться" в "private" DNS запись, а hostname вашей машины должен быть таким же, как у ближайшей галактики к нашей Солнечной системе (ну или выберете обычное скучное имя). Продемонстрируйте результаты с помощью  одной из утилит (dig, nslookup, host)


**3.** tcpdump и веселье:

   3.1 Подключаетесь по ssh ко второму интерфейсу машины, логинетесь.
   
   3.2 В одной сессии запускаете tcpdum, в другой сессии пытаетесь получить используя любой http клиент контент страницы по адресу: example.com
   
   3.2* Получите контент страницы с помощтью telnet
   
   3.3 В полученном выводе, найдите содержимое страницы и все HTTP заголовки.
   
   3.4 tcpdump команда должна быть максимально "узконаправленная", то есть, в выводе должно быть минимум трафика, не относящегося к цели задания.
  
**4.** Найдите номер порта, на котором запущен SSH сервер на хосте: 79.134.223.227 + все открытые порты.

***5.***
   Для выполнения этого задания вы должны получить доступ на хост с адресом: 45.88.76.32.
   
   Для этого вам необходимо передать открытую часть ключа преподавателю и после подтверждения подключиться по ssh к хосту.
   
   Цель задания: вам нужно найти сообщение в icmp трафике, который поступает на этот хост 42.88.76.32.   
   
   Предоставте сообщнеие в читаемом варианте и предоставте команду которой вы пользовались чтобы прочесть это сообщение. 
   
   Подсказка: вам доступен tcpdump (/usr/sbin/tcpdump) на хосте.
 
 
 </details>

 <details><summary>  Задания лекций 13-14 ( BASH )  </summary>

## Bash:
0. All scripts should be ran in debug mode.

1. Find a sum of all running process' PIDs.

2. A lucky number is one whose individual digits add up to 7, in successive additions. For example, 62431 is a lucky number (6 + 2 + 4 + 3 + 1 = 16, 1 + 6 = 7). Find all the lucky numbers between 1000 and 10000.

3. Write a script that takes a list of words (or even phrases) as an arguments. Script should ask a user to write something to stdin until user won't provide one of argument phrases.

example:
```
my_script.sh watermelon lemon apple
Enter my favourite word or phrase:
potato
No, it's not what I want!
Enter my favourite word or phrase:
cat
No, it's not what I want!
apple
Yes, this is my favourite word! Thank you, bye!
```

4. As bash doesn't have any syntax standardisation a lot of bash users develop scripts that make further readers very unhappy. Also, these guys often over engineers such scripts. This is an example of this script. Please analyse a script and try to make it as readable and functional as possible from your sense of beauty.
```
export SUM=0; for f in $(find src -name "*.java");
do export SUM=$(($SUM + $(wc -l $f | awk '{ print $1 }'))); done; echo $SUM
```

5. `stat` command shows when a particular file was accessed. Unfortunately, it can't show who it was. 
As a first step, you should study a Shell Variables section of man bash, enable an unlimited history size and time stamping of command execution.
As a second step*, provide a script that will get list of files as arguments, it should find a user who have last accessed each file and print a line in the following fashion `<filename> <user> <time>` and color it red if file was not just accessed but also modified.
__Note:__ this task is not about the development of an audit tool but about some play with bash. %)

\* Second step of a task may be treated as difficult and is optional

## RegExp:

To play:
https://alf.nu/RegexGolf
https://regexcrossword.com 

1. Stacktraces of JVM languages looks the following way:
```
	Caused by: org.apache.thrift.transport.TTransportException
	at org.apache.thrift.transport.TIOStreamTransport.read(TIOStreamTransport.java:132)
	at org.apache.thrift.transport.TTransport.readAll(TTransport.java:86)
	at org.apache.thrift.transport.TSaslTransport.receiveSaslMessage(TSaslTransport.java:178)
	at org.apache.thrift.transport.TSaslTransport.open(TSaslTransport.java:305)
	at org.apache.thrift.transport.TSaslClientTransport.open(TSaslClientTransport.java:37)
	at com.cloudera.hivecommon.api.HiveServer2ClientFactory.createTransport(Unknown Source)
	at com.cloudera.hivecommon.api.HiveServer2ClientFactory.createClient(Unknown Source)
	at com.cloudera.hivecommon.core.HiveJDBCCommonConnection.establishConnection(Unknown Source)
	at com.cloudera.impala.core.ImpalaJDBCConnection.establishConnection(Unknown Source)
	at com.cloudera.jdbc.core.LoginTimeoutConnection.connect(Unknown Source)
	at com.cloudera.jdbc.common.BaseConnectionFactory.doConnect(Unknown Source)
	at com.cloudera.jdbc.common.AbstractDriver.connect(Unknown Source)
	at org.apache.commons.dbcp2.DriverConnectionFactory.createConnection(DriverConnectionFactory.java:55)
	at org.apache.commons.dbcp2.PoolableConnectionFactory.makeObject(PoolableConnectionFactory.java:355)
	at org.apache.commons.dbcp2.BasicDataSource.validateConnectionFactory(BasicDataSource.java:115)
	at org.apache.commons.dbcp2.BasicDataSource.createPoolableConnectionFactory(BasicDataSource.java:665)
	at org.apache.commons.dbcp2.BasicDataSource.createDataSource(BasicDataSource.java:544)
	at org.apache.commons.dbcp2.BasicDataSource.getConnection(BasicDataSource.java:753)
	at org.apache.commons.dbutils.AbstractQueryRunner.prepareConnection(AbstractQueryRunner.java:319)
	at org.apache.commons.dbutils.QueryRunner.query(QueryRunner.java:345)
	at com.blah.nbs.validation.util.client.sql.AbstractSqlClient.lambda$executeQuery$0(AbstractSqlClient.java:55)
	at com.machinezoo.noexception.CheckedExceptionHandler$CheckedFunction.apply(CheckedExceptionHandler.java:723)
	at com.blah.nbs.validation.util.client.sql.AbstractSqlClient.lambda$executeSql$2(AbstractSqlClient.java:71)
	at java.util.concurrent.FutureTask.run(FutureTask.java:266)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)
```
1. Write a sed one-liner that will show stack traces lines in the following fashion:
```
You have a problem with entity org.apache.hadoop.fs.FileSystem$Cache.getInternal! You can find more info about it in file FileSystem.java at line 2703. This file is written on java.
```
2. Write a RegEx that validates entries under `/etc/passwd`.

3. \* (just if you're very interested :)). Write a RegEx that will validate URI: https://en.wikipedia.org/wiki/Uniform_Resource_Identifier
  </details>
 
 <details><summary>  Задания лекций 15-16 ( RPM/YUM, Files and file systems )  </summary>

task1:
	
	- Подключить репозиторий docker community edition
	- Установить docker-ce версии 19.03.14
	- Убедиться, что установлена нужная версия
	- Обновить docker-ce до последней версии
	- Вывести список последних операций yum
	- Вывести полную информацию об установленном ранее пакете
	- Удалить docker-ce

Task2:

	- Переместить mlocate.db в новое место
	- Создать новый файл file_task16.txt с любым содержанием и добавить информацию о нём в новый mlocate.db
	- Найти файл file_task16.txt через locate и вывести его содержимое на экран (без явного указания полного пути к файлу)
	- Создать хардлинк на file_task16.txt, назвать его file_task16_hard.txt
	- Внести любые изменения в file_task16.txt
	- Удалить file_task16.txt
	- Вывести на экран file_task16_hard.txt, убедиться, что в нём отражены изменения
	* Создать именованный пайп pipe01
	  В первом терминале запустить считывание с pipe01 (любым способом, можно перечислить несколько)
	  Создать софтлинк на пайп, назвать его pipe01-s
	  Во втором терминале отправить в pipe01-s данные (любым способом, можно перечислить несколько)
	  Убедиться, что данные были считаны первым терминалом
	  # mkfifo
	** Сделать то же самое, используя файл Unix socket (подсказка: используйте пакеты netcat и socat)
 </details>

<details><summary>  Задания лекций 17-18 ( Partitions and LVM )  </summary>

	1. Imagine you was asked to add new partition to your host for backup purposes. To simulate appearance of new physical disk in your server, please create new disk in Virtual Box (5 GB) and attach it to your virtual machine.
	Also imagine your system started experiencing RAM leak in one of the applications, thus while developers try to debug and fix it, you need to mitigate OutOfMemory errors; you will do it by adding some swap space.
	/dev/sdc - 5GB disk, that you just attached to the VM (in your case it may appear as /dev/sdb, /dev/sdc or other, it doesn't matter)
	1.1. Create a 2GB   !!! GPT !!!   partition on /dev/sdc of type "Linux filesystem" (means all the following partitions created in the following steps on /dev/sdc will be GPT as well)
	1.2. Create a 512MB partition on /dev/sdc of type "Linux swap"
	1.3. Format the 2GB partition with an XFS file system
	1.4. Initialize 512MB partition as swap space
	1.5. Configure the newly created XFS file system to persistently mount at /backup
	1.6. Configure the newly created swap space to be enabled at boot
	1.7. Reboot your host and verify that /dev/sdc1 is mounted at /backup and that your swap partition  (/dev/sdc2) is enabled

	2. LVM. Imagine you're running out of space on your root device. As we found out during the lesson default CentOS installation should already have LVM, means you can easily extend size of your root device. So what are you waiting for? Just do it!
	2.1. Create 2GB partition on /dev/sdc of type "Linux LVM"
	2.2. Initialize the partition as a physical volume (PV)
	2.3. Extend the volume group (VG) of your root device using your newly created PV
	2.4. Extend your root logical volume (LV) by 1GB, leaving other 1GB unassigned
	2.5. Check current disk space usage of your root device
	2.6. Extend your root device filesystem to be able to use additional free space of root LV
	2.7. Verify that after reboot your root device is still 1GB bigger than at 2.5.
	
</details>
<details><summary>  Задания лекций 19-20 ( Boot and iptables )  </summary>
	
Boot process:

1.* Self-study: find a utility to inspect initrd file contents. Find all files that are related to XFS filesystem and give a short description for every file.
	
2.* Self-study: explain the difference between ordinary and rescue initrdimages.
	
3.* Self-study: study dracut utility that is used for rebuilding initrd image. Give an example for adding driver/kernel module for your initrd and recreating it.

4.Enable recovery options for grub, update main configuration file and find newitem in GRUB2 config in /boot.

5.Modify option vm.dirty_ratio:a.using sysctl utilityb.using sysctl configuration file6.Disable selinux using kernel cmdlineiptables:With enabled firewalld:1.Add rule using firewall-cmd that will allow SSH access to your server *only* from network 192.168.56.0/24 and interface enp0s8 (if your network and/on interface name differs - change it accordingly).
	
5.2.Shutdown firewalld and add the same rules via iptables.
	
</details>

## Решения:
 
 <details><summary> Задания лекций 1-2 от 12.01.21 </summary>

 
 
 <details><summary> # 0.  </summary>
 
 
 
  Для начала создадим 2 виртуальные машины используя vitrualbox gui, в моем случае это Centos1 и Centos2 . 
  Имена пользователей аналогичны.
  
  В настройках виртуальных машин в virtualbox:
  
  У Centos1 установим 2 адаптера сети (bridge и internal network) - эта машина будет иметь доступ куда угодно, зададим второму адаптеру (internal network) имя сети "lan".
 
 Для второй машины будем использовать только 1 адаптер (internal network) ,аналогично 1ой , зададим имя сети "lan".

  После загрузки виртуальных машин зайдем на них , указав логин и пароль от соответствующей машины.
  Убедимся что наши сетевые интерфейсы доступны, выполним команду: 
  
  `ip a` .
  
  Следующий пункт. На каждой машине для интерфейса (internal network) отключим DHCP, настроим статический ip, укажем DNS, маску подсети , шлюз по-умолчанию.
  
  Для этого перейдем в директорию :
  
  `cd /etc/sysconfig/network-scripts`  
  
  С помощью редактора Vi отредактируем файл нужного нам интерфейса (в моем случае это enp0s3 и enp0s8):
  
  centos1:
  
  `sudo vi  ifcfg-enp0s3` .
  
  centos2:
  
  `sudo vi  ifcfg-enp0s8` .
  
  Редактируем строки: 

    BOOTPROTO	с dhcp на none
    DNS1	указажем dns сервер
    IPADDR0	настроим статический ip адрес
    PREFIX0	указажем маску подсети
    GATEWAY0 настроим шлюз по-умолчанию
  
  В итоге получим примерно такой вид файлов.
  
  Centos1:
  
   ![alt][logo]

[logo]:  https://github.com/outragee/epam-learning/blob/main/pics/centos1_networksetup.png "centos1"


  Centos2:
  
   ![centos2][logo2]
   
[logo2]: https://github.com/outragee/epam-learning/blob/main/pics/centos2_networksetups.png "centos2"


  Перезапустим службу сети на каждой из машин выполнив команду:

  `sudo systemctl restart network` .
  
  Теперь проверим что сетевые протоколы изменили свои настройки , а заодно попробуем попинговать одну машину на другую и попробуем кинуть ssh.
  Выполним следующие команды:
  
  `ip a` #проверим статус сетевых интерфейсов. 
  
  `ping 192.168.100.13`#Из centos2  или `ping 192.168.100.14` #из Centos1.
  
  `ssh 192.168.100.13` #для centos2 .14 ,соответственно.
  
  
  Вывод терминалов:
  
  centos2:
  
  ![out2][logo3]

[logo3]: https://github.com/outragee/epam-learning/blob/main/pics/centos2_allnetworks%2Bping.png "centos2"

  centos1:
  
  ![out3][logo4]

[logo4]: https://github.com/outragee/epam-learning/blob/main/pics/centos1_allnetworks%2Bping.png "centos1"

</details>



<details><summary> # 1.  </summary>

Для того ,чтобы найти все файлы содержащие "config" в имени ,в директории /usr/share/man ,включая поддиректории выполним команду ls ,совместно с пайплайном и командой grep. 

`ls /usr/share/man -a -R | grep config`

Где ls  - list директории, -а  - показать все файлы и директории,включаяя скрытые , -R -рекурсивно (все вложения) , | - пайплайн (конвеер ,передаст вывод комманды ls команде grep ) , grep -утилита коммандной строки,с помощью которой мы будем искать необходимые нам данные.

Вывод терминала:

 ![out4][logo5]

[logo5]: https://github.com/outragee/epam-learning/blob/main/pics/1lsconfig.png "ls+grep"  


Теперь мы одним вызовом ls найдем все файлы, содержащие слово "system" в каталогах /usr/share/man/man1 и /usr/share/man/man7
Для этого мы перечислим директории , лист которых будем производить и по аналогии выше - выполним grep слова system.

Вывод терминала:

![out5][logo6]

[logo6]: https://github.com/outragee/epam-learning/blob/main/pics/1systemgrep.png "ls++grep"  


</details>

<details><summary> # 2.  </summary>
 
Найдем в директории /usr/share/man все файлы, которые содержат слово "help" в имени,для этого используем команду:


`find /usr/share/man -iname "*help*"`


Найдем там же все файлы, имя которых начинается на "conf". Выполнив:


`find /usr/share/man -iname "conf*"`


Какие действия мы можем выполнить с файлами, найденными командой find (не запуская других команд)? Приведите любой пример с комментарием.
 
 
 
![out6][logo7]

[logo7]:  https://github.com/outragee/epam-learning/blob/main/pics/find.png "find"
 
Команда find очень обширна, кроме того ,можно использовать ее в связке с командой grep , что расширит и утончит поиск. Также ,для работы с найденными файлами мы можем использовать опцию -exec к примеру найдем как и выше вайлы ,где есть слово help и скопируем эти файлы в /home/centos1/test/ добавив им расширение .done :

`find . /usr/share/man -name '*help*' \-execdir cp {} /home/centos1/test/{}.done \;`

Вывод:

![out7][logo8]

[logo8]:  https://github.com/outragee/epam-learning/blob/main/pics/find-exec.png "find + exec"

По сути ,опция exec предоставляет очень обширные возможности для работы с файлами. Такие как- удаление,перемещение,изменение прав, использование bash - скрипта и другое.

 </details>

 <details><summary>  # 3. </summary>
 
  head и tail представлены 1ой командой,чтобы не делать 2 скрина.

![out8][logo9]

[logo9]: https://github.com/outragee/epam-learning/blob/main/pics/head%26tail.png "head&tail"


Если мы запросим больше строк,чем имеет файл,то head выдаст все те,что имеются и прекратит работу.

![out9][logo10]

[logo10]: https://github.com/outragee/epam-learning/blob/main/pics/wc%2Bheadmore.png "head more than file have"

  </details>
 
  <details><summary>  # 4. </summary>
 
![out10][logo11]

[logo11]: https://github.com/outragee/epam-learning/blob/main/pics/touchfiles.png "touch 1..3"

переименовывать файлы будем командой mv , хотя можно установить и rename :

    :~/test$ mv file_name1.md file_name1.textdoc
    :~/test$ mv file_name2.md file_name2
    :~/test$ mv file_name3.md  file_name3.md.latest
    :~/test$ mv file_name1.textdoc file_name1.txt

  </details>
 
 
  <details><summary>  # 5. </summary>
 
![out11][logo12]

[logo12]: https://github.com/outragee/epam-learning/blob/main/pics/cd.png "cd"

  </details>


  <details><summary>  # 6. </summary>
 
 Создаем директории, заодно перейдем в директорию new:
 
 `mkdir -p /home/outragee/epam-learning/{new,processed} /home/outragee/epam-learning/in-process/{tread0,tread1,tread2} && cd /home/outragee/epam-learning/new/`
 
 
 Создадим 100 файлов в директории, поскольку директория new/ текущая то:
 
 
 `touch /home/outragee/epam-learning/new/data{00..99}`
 
 
 Скопируем файлы в директории tread{0..2}/ :
 
 `cp /home/outragee/epam-learning/new/data{00..33} /home/outragee/epam-learning/in-process/tread0 & cp data{34..67} /home/outragee/epam-learning/in-process/tread1 & cp data{68..99} /home/outragee/epam-learning/in-process/tread2`

 
 Выведем содержимое каталога in-process:
 
 `ls -R /home/outragee/epam-learning/in-process/`
 
 
 Переместим файлы :
 
 
 `mv /home/outragee/epam-learning/in-process/tread{0..2}/* /home/outragee/epam-learning/processed/`
 
 
 Выведем содержимое каталога in-process и processed одной командой:
 
 
 `ls -a -R /home/outragee/epam-learning/in-process/ /home/outragee/epam-learning/processed/`
 
 
 Сравним количество файлов в каталогах new и processed , если они равны удалим файлы из new . Сравнение количества и удаление сделано при помощи условия того, что команда diff -q вернет нам 0 :
 
    if [ "$DIFF -q new/ processed/" != "0" ] ; then rm -r /home/outragee/epam-learning/new/* ; fi



![out13][logo14]

[logo14]: https://github.com/outragee/epam-learning/blob/main/pics/6full.png "full"

</details>

<details><summary>  # 7. </summary>


Для выполнения этого задания будем использовать цикл for в связке с коммандой seq (seq - это генератор чисел) .
Зададим переменные а=1 , b=3 , x=file . используем структуру цикла для каждой итерации генератора seq (который ограничен у нас переменными a=1 и b=3 эхо будет выводить в одной строке значение переменной x(file) и число, генерируемое seq . -n укажет echo вывод в одну строку. :


    a=1; b=3 ; x="file" ; for i in `seq  $a  $b `; do  echo -n  "$x $i "; done
    

![out12][logo13]

[logo13]: https://github.com/outragee/epam-learning/blob/main/pics/generation%20and%20for%20cycle.png "cycle_generation"


 </details>
 </details>









 <details><summary>  Задания лекций 3-4 (awk,sed,vim) </summary>
 
 <details><summary> AWK </summary>
 
 Чтобы узнать какой браузер чаще всего использовался будем считать повторы в столбце `$12` :
  
  
  `awk '{if (count [$ 12] ++ >= max) max = count [$ 12]} END {for (i in count) if (max == count [i]) print i, count [i]}' /home/outragee/epam/epam-learning/access.log `
  
 
 
    outragee@outragee-X220:~$ awk '{if (count [$ 12] ++ >= max) max = count [$ 12]} END {for (i in count) if (max == count [i]) print i, count [i]}' /home/outragee/epam/epam-learning/access.log 
    "Mozilla/4.0 43164

 
 
 Для поиска количества запросов от адреса ,необходимо задать условие с адресом в `$1` ,а так-же искомый месяц в `$4`.
 
 
 `awk  '  { if (($1 == "193.106.31.130") && (  $4 ~ "Dec" ))   print  "Dec count is:"count++ } ' access.log  | tail -1`
 
 
 
    outragee@outragee-X220:~/epam/epam-learning$ awk  '  { if (($1 == "193.106.31.130") && (  $4 ~ "Dec" ))   print  "Dec count is:"count++ } ' access.log  | tail -1
    Dec count is:10290
    awk  '  { if (($1 == "193.106.31.130") && (  $4 ~ "Jan" ))   print  "Jan count is:"count++ } ' access.log  | tail -1
    Jan count is:32378

 
 </details>
 
 <details><summary> SED </summary>
 
 Переименуем все агенты в Lynx. Мы знаем что в столбце 12 у нас находятся данные о пользовательских браузерах. Свяжем выбор по столбцу AWK и Sed:
 
 
    outragee@outragee-X220:~/epam/learning$ awk ' {print $12}' access.log | sed '/^"/c Lynx '   | head

    Lynx 
    Lynx 
    Lynx 
    Lynx 
    Lynx 
    Lynx 
    Lynx 
    Lynx 
    Lynx 
 Если в итоге мы хотим сохранить результат в файл то :
 
 `outragee@outragee-X220:~/epam/learning$ awk ' {print $12}' access.log | sed 's/^"/c Lynx /w output'  access.new`
 
 

 </details>
 </details>
 
 <details><summary>  Задания лекций 5-6 (users, groups, file access) </summary>

 

 <details><summary> TASK 1  </summary>



Заранее отредактируем файл /etc/login.defs .
изменим длительность действия пароля на 30 дней.


     PASS_MAX_DAYS 30


Создадим группу " sales " и присвоим ей GID 4000. 


`sudo groupadd -g 4000 sales`


Теперь создадим пользователей bob,alice,eve и обозначим группу sales как основную для них ,а так-же ограничим время существования аккаунтов до 90 дней.


`sudo useradd -g 4000 -e $(date -d "90 days" "+%Y-%m-%d") bob`

`sudo useradd -g 4000 -e $(date -d "90 days" "+%Y-%m-%d") alice`

`sudo useradd -g 4000 -e $(date -d "90 days" "+%Y-%m-%d") eve`


Зададим пароли пользователям и укажем длительность действия пароля,а так-же заставим их сразу поменять пароль, указав -n=1 .



`sudo passwd -n 1 -w 3 -x 30 bob`


`sudo passwd -n 1 -w 3 -x 30 alice`


`sudo passwd -n 1 -w 3 -x 30 eve`



Изменим срок действия пароля у пользователя bob. 


`sudo chage -M 15 bob`



</details>
 
  
 <details><summary> TASK 2 </summary>


Создадим группу students :


`sudo groupadd -g 1000 students`



Создадим 3х пользователей glen, antony, lesly добавим их в группу students.


`sudo useradd -g 1000 -e $(date -d "90 days" "+%Y-%m-%d") glen`


`sudo useradd -g 1000 -e $(date -d "90 days" "+%Y-%m-%d") antony`


`sudo useradd -g 1000 -e $(date -d "90 days" "+%Y-%m-%d") lesly`



Создадим директорию  /home/students :


`sudo mkdir /home/students `


Зайдем в директорию /home/students:

`cd /home/students`

Присвоим все файлы рекурсивно в директории /home/students группе students:


`sudo chown -R :students *`



Изменим права у директориии разрешим все владельцу и группе:



`sudo chmod -r ug+rwx /home/students`


Изменим права у директории, запретим всем остальным какие либо действия с директорией :


`sudo chmod o-rwx /home/students `



 </details>
 
 <details><summary> TASK 3 </summary>



Создадим общую директорию и файлы в ней.


`sudo mkdir /share/cases`


`touch murders.txt moriarty.txt`


Создадим 2 группы bakerstreet , scotlandyard:


`sudo groupadd -g 2000 bakerstreet`


`sudo groupadd -g 3000 scotlandyard`


Создадим пользователей holmes,watson,lestrade,gregson,jones :
 

`sudo useradd -g 2000 holmes`


`sudo useradd -g 2000 watson`


`sudo useradd -g 3000 lestrade`


`sudo useradd -g 3000 gregson`


`sudo useradd -g 3000 jones`



Создадим пароли пользователям:


`sudo passwd -n 15 -w 3 -x 30 holmes`

`sudo passwd -n 15 -w 3 -x 30 watson`

`sudo passwd -n 15 -w 3 -x 30 lestrade`

`sudo passwd -n 15 -w 3 -x 30 gregson`

`sudo passwd -n 15 -w 3 -x 30 jones`



Изменим владельца у общей директории :


`cd /share/cases && sudo chown -R :bakerstreet *`



Настроим права директории:


`sudo chmod -r ug+rw /share/cases`


`sudo chmod -r o-rwx /share/cases`


`sudo setfacl -m g:scotlandyard:rw /share/cases`



Дадим маску пользователю jones:


`sudo setfacl -m u:jones:r /share/cases`


 </details>
 </details>
 
 <details><summary>  Задания лекций 7-8 ( Process, systemd, cron/anacron, lsof ) </summary>
 
 <details><summary> Process </summary>
 
 
 Запустим команду sleep с 3мя разными интервалами времени 5 секунд,1 минута,15 секунд. пускай выводит список директории с ожиданием :
 
 `ls -a && sleep 5 && ls -a && sleep 15 && ls -a && sleep 1m`
 
 
 
 
 
Три варианта отправки сигнала SIGSTOP:
 
 
 
При помощи сочетаний клавиш ,в текущем выполняемом задании нажать `CTRL+C` , `CTRL+Z`. 

При помощи команды `kill` с указанием PID процесса и номера сигнала (у SIGSTOP это 17,19,23) (для SIGKILL 9) :

`kill -17 2500`  - остановит процесс с PID 2500 
        
при помощи команды killall (аналогична kill ,но указывается имя процесса ,а не PID):

`killall -19 chromium`





Запустим процесс и переместим в бэкграунд :

`sleep 10m && echo done` CTRL+C

`bg`

Запустим процесс top , а затем остановим его :

`top`

`killall -19 top`

Проверим статус выполнив `jobs -l` : 

       outragee@outragee-X220:~$ jobs -l
       [1]+ 93456 Stopped (signal)        top
       [2]- 95868 Running                 sleep 10m &

Выполним команду `fg` (если джоб больше одной ,то можно испльзовать совместно с %# `fg % #job id` , пошлет сигнал SIGCONT:


`FG` это вернет нам остановленный процесс `top` .


Для передачи сигнала SIGCONT выполним:


`kill -SIGCONT 96456`


Убьем один процесс по PID и по Job ID, для этого опять вызовим листинг `job -l` :

          
          outragee@outragee-X220:~$ jobs -l
          [1]+ 93456 Stopped (signal)        top


Чтобы убить по ID выполним команду  `kill -9 93456`  чтобы убить по job ID выполним  `kill -9 %1`


 </details>
 <details><summary> Systemd </summary>
 Для начала напишем 2 скрипта , 1ый будет выдавать текущую дату , писать что демон запушен в это время и затем уходить в sleep , по завершению sleep отправлять 1 в файл(лог) . Второй демон будет совсем простой , он напишет дату, когда он будет выполнен и отправит 2 в файл(лог). Укажем,что демон 2 и таймер запускаются после сервиса daemon1 . Напишем таймер и зададим ему дату срабатывания.
 
*Daemon 1*:
 
        #!/bin/bash

        #print 
        echo "daemon 2 started at:"

        # start time
        date +"%H:%M:%S"

        # sleep for 10sec
        sleep 10

        # do echo like log file
        echo 1 > /tmp/homework


*Daemon 2*:
        

        #!/bin/bash


        #print 
        echo "daemon 2 oneshoted at:"

        # start time
        date +"%H:%M:%S"

        echo 2 > /tmp/homework


*Unit file daemon 1* :
         
       [Unit]
       Description=daemon 1 unit
       After=network.target

       [Service]
       Type=simple
       PIDFile=/home/outragee/epam/epam-learning/daemon1.pid
       WorkingDirectory=/home/outragee/epam/epam-learning

       User=outragee
       Group=outragee

       OOMScoreAdjust=-100

       ExecStart=/usr/sbin/d1.sh   
       ExecStop=/bin/kill -15 $MAINPID 
       TimeoutSec=300

       [Install]
       WantedBy=multi-user.target 


*Unit file daemon 2* :

      
       [Unit]
       Description=daemon 2 unit
       After=daemon1.service
       Require=daemon1.service
       
       [Service]
       Type=oneshot
       ExecStart=/usr/sbin/d2.sh
       RemainAfterExit=yes
       
       User=outragee
       Group=outragee

       [Install]
       WantedBy=multi-user.target
       

*Timer* :
       
       
       [Unit]
       Description= Timer for daemon2
       After=daemon1.service

       [Timer]
       OnCalendar=2019-01-01

       [Install]
       WantedBy=timers.target

 
 Поместим юнит файлы в директорию `/etc/systemd/system` и изменим права у файлов:
 
 
 `sudo chmod 755 daemon1.service daemon2.service daemon2.timer` 
 
 
 Теперь запустим наших демонов и убедимся что все работает как должно:



![out14][logo15]


[logo15]: https://github.com/outragee/epam-learning/blob/main/pics/status.png "daemon status check"



Посмотрим вывод файла `/tmp/homework`:
        
        
        outragee@outragee-X220:/tmp$ cat /tmp/homework 
        1


 </details>
 
 <details><summary> Cron/anacron </summary> 
 
 **1.** Создадим джобу,которая будет выполнять запуск нашего скрипта. В центос есть таблица `/etc/anacrontab` аналогичная таблице crontab. Зайдем  и создадим в ней задание:
 
 `sudo vim \etc\anacrontab`
 
    # /etc/anacrontab: configuration file for anacron

    # See anacron(8) and anacrontab(5) for details.

    SHELL=/bin/sh
    PATH=/sbin:/bin:/usr/sbin:/usr/bin
    MAILTO=root
    # the maximal random delay added to the base delay of the jobs
    RANDOM_DELAY=45
    # the jobs will be started during the following hours only
    START_HOURS_RANGE=3-22

    #period in days   delay in minutes   job-identifier   command
    1       5       cron.daily              nice run-parts /etc/cron.daily
    7       25      cron.weekly             nice run-parts /etc/cron.weekly
    2       1       cron.every2days         nice run-parts /etc/cron.every2days
    @monthly 45     cron.monthly            nice run-parts /etc/cron.monthly
 
 Теперь создадим директорию `/etc/cron.every2days/` и файл `echosender.sh` :
 
 `sudo vim /etc/cron.every2days/echosender.sh`
 
 И отредактируем его:

 
    #!/bin/bash
    echo "Hello" > /opt/hello

 В завершении ,проверим имеются ли ошибки если вывод пуст,то их нет:
 
 `anacron -T`
 
 **2.**
 Для начала создадим резервную копию имеющегося файла crontab , просто скопировав его и добавив .bak. Затем запишем новое задание :
 
 `crontab -e`
 
 `@reboot sleep 60 && /etc/cron.every2days/echosender.sh`

 
 </details>
 

 <details><summary> Lsof </summary> 
 
 **1.**
 
 `sleep 2m  2>stderr.log 1>stdout.log`
 
 **2.**
 
    
    outragee@outragee-X220:~$ lsof /home/outragee/stdout.log 
    COMMAND   PID     USER   FD   TYPE DEVICE SIZE/OFF    NODE NAME
    sleep   11106 outragee    1w   REG    8,2        0 4198453 /home/outragee/stdout.log
    outragee@outragee-X220:~$ lsof /home/outragee/stderr.log 
    COMMAND   PID     USER   FD   TYPE DEVICE SIZE/OFF    NODE NAME
    sleep   11106 outragee    2w   REG    8,2        0 4198449 /home/outragee/stderr.log

 
 
 **3.**
 
 Для выполнения этого заданя , укажем флаги -ipv4 -ipv6 и tcp ip:
 
 `lsof -a -i4 -i6 -itcp`
 
    outragee@outragee-X220:~$ lsof -a -i4 -i6 -itcp
    COMMAND    PID     USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
    ignition- 2974 outragee    6u  IPv4  46010      0t0  TCP localhost:32000->localhost:31000 (ESTABLISHED)
    java      3092 outragee    4u  IPv4  48012      0t0  TCP localhost:32000 (LISTEN)
    java      3092 outragee   93u  IPv6  46007      0t0  TCP localhost:31000->localhost:32000 (ESTABLISHED)
    java      3092 outragee   99u  IPv6  51220      0t0  TCP *:omniorb (LISTEN)
    chrome    8422 outragee   29u  IPv4  71186      0t0  TCP outragee-X220:48522->lb-140-82-112-25-iad.github.com:https (ESTABLISHED)
    chrome    8422 outragee   30u  IPv4  72164      0t0  TCP outragee-X220:49548->220.165.107.34.bc.googleusercontent.com:https (ESTABLISHED)
    chrome    8422 outragee   60u  IPv4  62841      0t0  TCP outragee-X220:41384->lh-in-f188.1e100.net:5228 (ESTABLISHED)
    chrome    8422 outragee   62u  IPv4  72183      0t0  TCP outragee-X220:58694->151.101.84.193:https (ESTABLISHED)
    chrome    8422 outragee   65u  IPv4  71376      0t0  TCP outragee-X220:35202->151.101.65.69:https (ESTABLISHED)
    chrome    8422 outragee   68u  IPv4  72184      0t0  TCP outragee-X220:33874->192.0.73.2:https (ESTABLISHED)
    chrome    8422 outragee   76u  IPv4  70410      0t0  TCP outragee-X220:35212->151.101.65.69:https (ESTABLISHED)
    chrome    8422 outragee   77u  IPv4  70889      0t0  TCP outragee-X220:35700->104.244.42.136:https (ESTABLISHED)

 

 
 </details>
 </details>

 
 
 
 <details><summary> Задания лекций 9-10 (SSH , timezone , logs ) </summary> 
 
 <details><summary>  SSH </summary> 
Зайдем на хост и выйдем:

    outragee@outragee-X220:~$ ssh Ivan_Rigalin@40.68.74.188 
    The authenticity of host '40.68.74.188 (40.68.74.188)' can't be established.
    ECDSA key fingerprint is SHA256:4r72O0/zt+DU9bsD85l3ZeMMYDlDRTv9h4KWBMoekKY.
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
    Warning: Permanently added '40.68.74.188' (ECDSA) to the list of known hosts.
    Password: 
    Password: 
    Last failed login: Mon Feb  1 07:26:00 UTC 2021 from 176.59.97.147 on ssh:notty
    There was 1 failed login attempt since the last successful login.
    [Ivan_Rigalin@vm-one ~]$ 
    [Ivan_Rigalin@vm-one home]$ logout
    Connection to 40.68.74.188 closed.



Отредактируем файл конфига:
    
    Host epam
        Hostname 40.68.74.188
        User Ivan_Rigalin
        port 22
        IdentityFile ~/.ssh/hw-5


        
Создадим новую пару ключей, старые предварительно лучше бы копирнуть.

    outragee@outragee-X220:~/.ssh$ ssh-keygen 
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/outragee/.ssh/id_rsa): hw-5
    Enter passphrase (empty for no passphrase): 
    Enter same passphrase again: 
    Your identification has been saved in hw-5
    Your public key has been saved in hw-5.pub
    The key fingerprint is:
    SHA256:mtHGI7uwYObQz2ghM1BOc7zjFeN1hUD4X7vEtSVa6Do outragee@outragee-X220
    The key's randomart image is:
    +---[RSA 3072]----+
    |   .   oo. o.    |
    |  + o + . o      |
    | + o o = .   .   |
    |. . o oo.   o + .|
    |.  . oo S. + = + |
    |+.. .  B .. * .  |
    |.+=.. +    o .   |
    | =.= o .  E .    |
    | .o + .    .     |
    +----[SHA256]-----+
    outragee@outragee-X220:~/.ssh$ ls
    config  hw-5  hw-5.pub  id_rsa  id_rsa.bak  id_rsa.pub  id_rsa.pub.bak  known_hosts



Зальем ключ на сервер , проверим ,работает ли вход без пароля :

    outragee@outragee-X220:~/.ssh$ ssh-copy-id -i ~/.ssh/hw-5 Ivan_Rigalin@40.68.74.188
    /usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/outragee/.ssh/hw-5.pub"
    /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
    /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
    Password: 

    Number of key(s) added: 1

    Now try logging into the machine, with:   "ssh 'Ivan_Rigalin@40.68.74.188'"
    and check to make sure that only the key(s) you wanted were added.

    outragee@outragee-X220:~/.ssh$ ssh epam   
    Last login: Mon Feb  1 07:56:13 2021 from 176.59.97.147
    [Ivan_Rigalin@vm-one ~]$ 
    [Ivan_Rigalin@vm-one ~]$ logout
    Connection to 40.68.74.188 closed.

#Имея приватную часть ключа можно сгенерировать публичную часть# 

`ssh-keygen -y -f ~/.ssh/key > ~/.ssh/key.pub`


Проверим ,есть ли сервис на 80 порту:
    
    [Ivan_Rigalin@vm-one ~]$ curl -v telnet://10.0.0.5:80
    * About to connect() to 10.0.0.5 port 80 (#0)
    *   Trying 10.0.0.5...
    * Connected to 10.0.0.5 (10.0.0.5) port 80 (#0)
    
    outragee@outragee-X220:~/.ssh$ nmap -Pn 40.68.74.188 -p 80
    Starting Nmap 7.80 ( https://nmap.org ) at 2021-02-01 11:20 MSK
    Nmap scan report for 40.68.74.188
    Host is up.

    PORT   STATE    SERVICE
    80/tcp filtered http

    Nmap done: 1 IP address (1 host up) scanned in 2.27 seconds



 Теперь пробросим порт и проверим доступность из локалки:
 
    outragee@outragee-X220:~/.ssh$ ssh -L 9999:localhost:80 Ivan_Rigalin@40.68.74.188
    Last login: Mon Feb  1 08:38:44 2021 from 176.59.97.147

    outragee@outragee-X220:~/.ssh$ curl -v telnet://localhost:9999
    
    *   Trying 127.0.0.1:9999...
    * TCP_NODELAY set
    * Connected to localhost (127.0.0.1) port 9999 (#0)


 
 Бонус :
 
 Делаем форвард до локальной машины внутри сети :
    
    ssh -L 9999:10.0.0.5:80 epam
    Last login: Mon Feb  1 08:40:14 2021 from 176.59.97.147
    [Ivan_Rigalin@vm-one ~]$ 
    
    

Теперь откроем наш браузер и напишем адрес ` http://localhost:9999/ ` :




![out15][logo16]


[logo16]: https://github.com/outragee/epam-learning/blob/main/pics/ngnx.png "nginx output"


</details>

<details><summary>  TASK 2 </summary> 

Сменим часовой пояс:

    outragee@outragee-X220:~/epam/epam-learning$ timedatectl list-timezones | grep Havana
    America/Havana
    outragee@outragee-X220:~/epam/epam-learning$ cat /etc/timezone 
    Europe/Moscow
    outragee@outragee-X220:~/epam/epam-learning$ timedatectl list-timezones | grep Havana
    America/Havana
    outragee@outragee-X220:~/epam/epam-learning$ sudo timedatectl set-timezone America/Havana 

Теперь поищем измененные журналы на локалхосте за последние 50 минут , от пользователя с id 81:

    outragee@outragee-X220:~/epam/epam-learning$ journalctl _UID=81 -u localhost --since "50 min ago"  --until "now"
    -- Logs begin at Mon 2020-10-26 07:22:23 MSK, end at Mon 2021-02-01 13:23:47 MSK. --
    -- No entries --
    
   


</details>
</details>


</details>

<details><summary> Задания лекций 11-12. ( Networking ) </summary> 
 
 <details><summary> Task#1 (nmcli + dnsmasq)  </summary> 

 
 Посмотрим какие есть интерфейсы выберем нужный нам- основной `enp0s3` :
 
    2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:23:99:7d brd ff:ff:ff:ff:ff:ff
    inet 192.168.43.104/24 brd 192.168.43.255 scope global noprefixroute dynamic enp0s3

 Через nmcli :
 
    [centos1@centos1 ~]$ nmcli d s
    DEVICE  TYPE      STATE         CONNECTION 
    enp0s3  ethernet  connected     enp0s3     
    enp0s8  ethernet  disconnected  --         
    lo      loopback  unmanaged     --  
 
    [centos1@centos1 ~]$ nmcli c s
    NAME    UUID                                  TYPE      DEVICE 
    enp0s3  f19d5aac-d9aa-4c81-a39e-145fdca9964a  ethernet  enp0s3 
    enp0s8  b0f69025-bb04-47aa-9dd3-024488bec2bf  ethernet  --     

Теперь добавим второй ip для enp0s3:
    
    nmcli c d enp0s3   # отключаем конект
    nmcli c m enp0s3 +ipv4.addresses "10.0.0.1\30"  # добавляем второй адрес с маской 255.255.255.252 в подсети будет 2 адреса 
    nmcli c m enp0s3 +ipv4.routes "10.0.0.1\30 192.168.43.255" # роутим сеть к шлюзу 
    nmcli c m enp0s3 +ipv4.dns "192.168.43.1 8.8.8.8 8.8.4.4" # добавим днс 
    nmcli c u enp0s3 # включим коннект
    
Зададим hostname и отредактируем файл /etc/hosts :

    hostnamectl set-hostname andromeda
    sudo vi /etc/hosts
    
    #добавим адрес
    10.0.0.1    andromeda.laba andromeda
    127.0.0.1       localhost
    
Для выполнения резолва в частный днс установим Dnsmasq:
`sudo yum install dnsmasq`

Теперь настроим dnsmasq и перезапустим сервис:

`sudo vim /etc/dnsmasq.conf`


    server=8.8.8.8
    local=/localnet/
    address=/andromeda.laba/10.0.0.1
     

`sudo systemctl restart dnsmasq`


Для того, чтобы обращения к DNS шли именно на dnsmasq на том же сервере, где он сам работает, необходимо указать первой записью в /etc/resolv.conf следующую строку:

    nameserver 127.0.0.1


Выполним поиск используя nslookup: 

    [centos1@andromeda ~]$ nslookup andromeda.laba
    Server:		127.0.0.1
    Address:	127.0.0.1#53

    Name:	andromeda.laba
    Address: 10.0.0.1

</details>

<details><summary> Task#2 (tcpdump and partyhard) </summary> 
 
 Зайдем на второй адрес по ssh:
 
    outragee@outragee-X220:~$ ssh vm
    centos1@192.168.0.18's password: 
    Last login: Tue Feb  9 09:40:33 2021 from andromeda.laba
    [centos1@andromeda ~]$ ssh centos1@10.0.0.1
    centos1@10.0.0.1's password: 
    Last login: Tue Feb  9 12:46:47 2021 from 192.168.0.16
    [centos1@andromeda ~]$ 

Запустим TCPDUMP:
   
    [centos1@andromeda ~]$ sudo tcpdump  -p -t -i enp0s3 port 80 -vv
    [sudo] password for centos1: 
    tcpdump: listening on enp0s3, link-type EN10MB (Ethernet), capture size 262144 bytes

Выполним запрос :


`curl www.example.com`

Через telnet: 

   
    telnet www.example.com 80
    GET /index.html HTTP/1.1
    Host: www.example.com
    ## в конце 2 раза энтер.
 

И посмотрим снова в 1 терминал:
<details><summary> простыня TCPDUMP  </summary>
   




    IP (tos 0x10, ttl 64, id 32785, offset 0, flags [DF], proto TCP (6), length 60)
    andromeda.33468 > 93.184.216.34.http: Flags [S], cksum 0xf6c3 (incorrect -> 0x0dea), seq 1853599587, win 29200, options [mss 1460,sackOK,TS val 18034546 ecr 0,nop,wscale 7], length 0
    IP (tos 0x0, ttl 55, id 25329, offset 0, flags [none], proto TCP (6), length 60)
    93.184.216.34.http > andromeda.33468: Flags [S.], cksum 0xedb1 (correct), seq 542252167, ack 1853599588, win 65535, options [mss 1452,sackOK,TS val 672935240 ecr 18034546,nop,wscale 9], length 0
    IP (tos 0x10, ttl 64, id 32786, offset 0, flags [DF], proto TCP (6), length 52)
    andromeda.33468 > 93.184.216.34.http: Flags [.], cksum 0xf6bb (incorrect -> 0x1afa), seq 1, ack 1, win 229, options [nop,nop,TS val 18034699 ecr 672935240], length 0
    IP (tos 0x10, ttl 64, id 32787, offset 0, flags [DF], proto TCP (6), length 78)
    andromeda.33468 > 93.184.216.34.http: Flags [P.], cksum 0xf6d5 (incorrect -> 0xd3b3), seq 1:27, ack 1, win 229, options [nop,nop,TS val 18072188 ecr 672935240], length 26: HTTP, length: 26
	GET /index.html HTTP/1.1
    IP (tos 0x0, ttl 55, id 30345, offset 0, flags [none], proto TCP (6), length 52)
    93.184.216.34.http > andromeda.33468: Flags [.], cksum 0xf5ca (correct), seq 1, ack 27, win 128, options [nop,nop,TS val 672972880 ecr 18072188], length 0
    IP (tos 0x10, ttl 64, id 32788, offset 0, flags [DF], proto TCP (6), length 76)
    andromeda.33468 > 93.184.216.34.http: Flags [P.], cksum 0xf6d3 (incorrect -> 0x60d9), seq 27:51, ack 1, win 229, options [nop,nop,TS val 18085924 ecr 672972880], length 24: HTTP
    IP (tos 0x0, ttl 55, id 32383, offset 0, flags [none], proto TCP (6), length 52)
    93.184.216.34.http > andromeda.33468: Flags [.], cksum 0x8a62 (correct), seq 1, ack 51, win 128, options [nop,nop,TS val 672986616 ecr 18085924], length 0
    IP (tos 0x10, ttl 64, id 32789, offset 0, flags [DF], proto TCP (6), length 54)
    andromeda.33468 > 93.184.216.34.http: Flags [P.], cksum 0xf6bd (incorrect -> 0x7770), seq 51:53, ack 1, win 229, options [nop,nop,TS val 18087325 ecr 672986616], length 2: HTTP
    IP (tos 0x0, ttl 55, id 32534, offset 0, flags [none], proto TCP (6), length 52)
    93.184.216.34.http > andromeda.33468: Flags [.], cksum 0x7f6e (correct), seq 1, ack 53, win 128, options [nop,nop,TS val 672988017 ecr 18087325], length 0
    IP (tos 0x0, ttl 55, id 32535, offset 0, flags [none], proto TCP (6), length 1664)
    93.184.216.34.http > andromeda.33468: Flags [P.], cksum 0xfd07 (incorrect -> 0x1b4b), seq 1:1613, ack 53, win 128, options [nop,nop,TS val 672988018 ecr 18087325], length 1612: HTTP, length: 1612
	   HTTP/1.1 200 OK
	   Accept-Ranges: bytes
	   Age: 454786
	   Cache-Control: max-age=604800
	   Content-Type: text/html; charset=UTF-8
	   Date: Tue, 09 Feb 2021 18:24:36 GMT
	   Etag: "3147526947+gzip"
	   Expires: Tue, 16 Feb 2021 18:24:36 GMT
	   Last-Modified: Thu, 17 Oct 2019 07:18:26 GMT
	   Server: ECS (dcb/7F83)
	   Vary: Accept-Encoding
	   X-Cache: HIT
	   Content-Length: 1256
	
	   <!doctype html>
	   <html>
	   <head>
	       <title>Example Domain</title>
	
	       <meta charset="utf-8" />
	       <meta http-equiv="Content-type" content="text/html; charset=utf-8" />
	       <meta name="viewport" content="width=device-width, initial-scale=1" />
	       <style type="text/css">
	       body {
	           background-color: #f0f0f2;
	           margin: 0;
	           padding: 0;
	           font-family: -apple-system, system-ui, BlinkMacSystemFont, "Segoe UI", "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
	        
	       }
	       div {
	           width: 600px;
	           margin: 5em auto;
	           padding: 2em;
	           background-color: #fdfdff;
	           border-radius: 0.5em;
	           box-shadow: 2px 3px 7px 2px rgba(0,0,0,0.02);
	       }
	       a:link, a:visited {
	           color: #38488f;
	           text-decoration: none;
	       }
	       @media (max-width: 700px) {
	           div {
	               margin: 0 auto;
	               width: auto;
	           }
	       }
	       </style>    
	   </head>
	
	   <body>
	   <div>
	       <h1>Example Domain</h1>
	       <p>This domain is for use in illustrative examples in documents. You may use this
	       domain in literature without prior coordination or asking for permission.</p>
	       <p><a href="https://www.iana.org/domains/example">More information...</a></p>
	   </div>
	   </body>
	   </html>
    IP (tos 0x10, ttl 64, id 32790, offset 0, flags [DF], proto TCP (6), length 52)
    andromeda.33468 > 93.184.216.34.http: Flags [.], cksum 0xf6bb (incorrect -> 0x780b), seq 53, ack 1613, win 254, options [nop,nop,TS val 18087477 ecr 672988018], length 0


</details>
</details>

<details><summary>  nmap (найти все открытые порты на удаленной машине) </summary>

Выполним сканирование всех портов ( некрасиво и медленно ):
	
	outragee@outragee-X220:~$ sudo nmap -Pn -p- 79.134.223.227
	Starting Nmap 7.80 ( https://nmap.org ) at 2021-02-16 15:18 MSK
	Nmap scan report for 79-134-223-227.obit.ru (79.134.223.227)
	Host is up (0.022s latency).
	Not shown: 65534 filtered ports
	PORT      STATE SERVICE
	60022/tcp open  unknown
	
	Nmap done: 1 IP address (1 host up) scanned in 11626.06 seconds

	

</details>


<details><summary>  TCPDUMP + ICMP on remote host 45.88.76.32 </summary>

Зайдем на хост выполнив ssh,
Посмотрим интерфейсы  найдем интересующий нас адрес:

`ip a`
	
	2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000


	



 От лица суперпользователя выполним tcpdump:
 
Укажем флаги : -A - сообщения в ASCII формате , -tttt human readable , -vv verbosity ,  -S - позволяет не обрабатывать абсолютные порядковые номера в относительные и -nn 	отображать IP адреса и номера портов вместо имени хостов и названия протоколов. Укажем что нас интересует icmp и только поступающий на хост dst host 45.88.76.32.

`sudo /usr/sbin/tcpdump -A -ttttnnvvS -i eth0 icmp and dst host 45.88.76.32`
 
 	2021-02-16 11:40:06.038848 IP (tos 0x0, ttl 34, id 0, offset 0, flags [none], proto ICMP (1), length 84)
    	35.180.189.228 > 45.88.76.32: ICMP echo request, id 5, seq 17194, length 64
	E..T....".=.#...-XL ...:..C*.d7.....................................................
	2021-02-16 11:40:11.163837 IP (tos 0x0, ttl 34, id 0, offset 0, flags [none], proto ICMP (1), length 84)
    	35.180.110.164 > 45.88.76.32: ICMP echo request, id 11, seq 2267, length 64
	E..T...."...#.n.-XL .........d7.....................................................
	2021-02-16 11:40:19.176687 IP (tos 0x0, ttl 34, id 0, offset 0, flags [none], proto ICMP (1), length 84)
    	35.180.169.86 > 45.88.76.32: ICMP echo request, id 17, seq 4533, length 64
	E..T....".R'#..V-XL ..w......d7..I3X................................................
	2021-02-16 11:40:19.848917 IP (tos 0x0, ttl 34, id 0, offset 0, flags [none], proto ICMP (1), length 84)
    	35.180.119.108 > 45.88.76.32: ICMP echo request, id 1, seq 5235, length 64
	E..T...."...#.wl-XL ..-....s.d7..DR.................................................
	2021-02-16 11:40:28.581583 IP (tos 0x0, ttl 34, id 0, offset 0, flags [none], proto ICMP (1), length 84)
    	15.188.77.34 > 45.88.76.32: ICMP echo request, id 30, seq 8848, length 64
	E..T...."..S..M"-XL ...H.."..d7.....................................................
	2021-02-16 11:40:34.239863 IP (tos 0x0, ttl 34, id 0, offset 0, flags [none], proto ICMP (1), length 84)
    	52.47.132.237 > 45.88.76.32: ICMP echo request, id 13, seq 6228, length 64
	E..T....".f.4/..-XL ..q....T.d7.o...................................................

 </details>


</details>
</details>

 <details><summary> Задания лекций 13-14 ( BASH )   </summary>    
 
 ##1.## Find a sum of all running process' PIDs. Объединим через пайп ps aux и awk ,авк укажем столбец с pidами .

	outragee@outragee-X220:~/epam$ ps aux | awk '{s+=$2}END{print s}'
	3943879

 ##3.## Напишем скрипт ,он будет выполняться в цикле,пока пользователь не введет верный ответ.
 Скрипт :
 
 	#!/bin/bash

	echo -n "Enter my favorite word or phrase: "
	read -r string
	while [[ "$string" != "apple" ]]; do
        	echo "No, it's not what I want! Please try again"
        	read -r string
	done
	if [[ $string = "apple" ]]
	then
  	  	echo "Yes , this is my favorite word! Thank you, bye!"
	fi
Выполним:
	
	[centos1@andromeda ~]$ ./test1.sh 
	Enter my favorite word or phrase: afa
	No, it's not what I want! Please try again
	123
	No, it's not what I want! Please try again
	!
	No, it's not what I want! Please try again
	apple
	Yes , this is my favorite word! Thank you, bye!

##4.## 
Перепишем скрипт :

	#!/bin/bash
	export SUM;
	for f in $(find . -name "*.java");do
 	 num=$(($SUM + $(wc -l $f | awk '{ print $1 }')))
	done
	echo "Количество строк во всех файлах java = " $num 

	[centos1@andromeda ~]$ ./vision.sh 
	Количество строк во всех файлах java =  6

 </details>
 

 
 <details><summary> Задания лекций 15-16 ( RPM/YUM, Files and file systems )  </summary>
 
 <details><summary> task1 </summary>
 Установим yum-utils пакет который предоставляет yum-config-manager утилиту и добавим стабильный репозиторий.


`sudo yum install -y yum-utils`
`sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo`
  
 
 Выполним установку нужной версии докера : 
 

`sudo yum install docker-ce-19.03.14-3.el7 docker-ce-cli-19.03.14-3.el7 containerd.io`


 Проверим версию:

	[centos1@andromeda ~]$ docker -v
	Docker version 19.03.14, build 5eb3275d40
	
	
Обновим все пакеты (хотя можно обновить только докер ) и проверим версию докера снова:
 	
	[centos1@andromeda ~]$ docker -v
	Docker version 20.10.3, build 48d30b5

Посмотрим последние операции в yum:

	[centos1@andromeda ~]$ sudo yum history 
	[sudo] password for centos1: 
	Loaded plugins: fastestmirror
	ID     | Login user               | Date and time    | Action(s)      | Altered
	-------------------------------------------------------------------------------
    	14 | centos1 <centos1>        | 2021-02-16 09:46 | I, U           |   81   
    	13 | centos1 <centos1>        | 2021-02-16 09:43 | Install        |    3   
    	12 | centos1 <centos1>        | 2021-02-16 09:41 | Erase          |    3   
    	11 | centos1 <centos1>        | 2021-02-16 09:40 | Install        |    3   
    	10 | centos1 <centos1>        | 2021-02-16 09:39 | Erase          |    4   
     	9 | centos1 <centos1>        | 2021-02-16 09:28 | Install        |   15   
     	8 | centos1 <centos1>        | 2021-02-16 09:27 | Install        |    4   
     	7 | centos1 <centos1>        | 2021-02-09 10:01 | Install        |    1   
     	6 | centos1 <centos1>        | 2021-02-09 09:47 | Install        |    2   
     	5 | centos1 <centos1>        | 2021-02-09 09:00 | Install        |   31   
     	4 | centos1 <centos1>        | 2021-02-09 08:22 | Install        |    2   
     	3 | centos1 <centos1>        | 2021-02-05 06:52 | Install        |    6   
     	2 | centos1 <centos1>        | 2021-02-05 04:13 | Install        |    1   
     	1 | System <unset>           | 2021-02-05 03:24 | Install        |  301   
	history list
	[centos1@andromeda ~]$ 


Удалим docker:


`sudo yum remove docker-ce docker-ce-cli containerd.io`

	Removed:
  	containerd.io.x86_64 0:1.4.3-3.1.el7  docker-ce.x86_64 3:20.10.3-3.el7  docker-ce-cli.x86_64 1:20.10.3-3.el7 

	Dependency Removed:
  	docker-ce-rootless-extras.x86_64 0:20.10.3-3.el7     


`sudo rm -rf /var/lib/docker`


Посмотрим сведения о пакете docker:

	[centos1@andromeda ~]$ yum info docker
	Loaded plugins: fastestmirror
	Loading mirror speeds from cached hostfile
 	* base: mirror.logol.ru
 	* extras: centos-mirror.rbc.ru
 	* updates: centos-mirror.rbc.ru
	Available Packages
	Name        : docker
	Arch        : x86_64
	Epoch       : 2
	Version     : 1.13.1
	Release     : 203.git0be3e21.el7.centos
	Size        : 18 M
	Repo        : extras/7/x86_64
	Summary     : Automates deployment of containerized applications
	URL         : https://github.com/docker/docker
	License     : ASL 2.0
	Description : Docker is an open-source engine that automates the deployment of any
        	    : application as a lightweight, portable, self-sufficient container that will
            	: run virtually anywhere.
           	 : 
            	: Docker containers can encapsulate any payload, and will run consistently on
            	: and between virtually any server. The same container that a developer builds
            	: and tests on a laptop will run at scale, in production*, on VMs, bare-metal
           	 : servers, OpenStack clusters, public instances, or combinations of the above.


 </details>
 
 <details><summary> task2 </summary>
 
 Поскольку Locate db у меня вообще не была установлена , то :
 
 
 `sudo yum install mlocate -y`
 
 
 Теперь создадим файл c содержанием:
 
 
 `vim /home/centos1/file_task16.txt`
 
 	test example locate
 
 
 Обновим данные базы данных:
 
 
 `sudo updatedb`
 
 
 Узнаем где у нас находится наш созданный файл используя locate:
 
 	
	[centos1@andromeda ~]$ locate file_task16.txt 
	/home/centos1/file_task16.txt

Создадим хардлинк:

	[centos1@andromeda ~]$ ln /home/centos1/file_task16.txt /home/centos1/file_task16_hard.txt
	[centos1@andromeda ~]$ ls
	file_task16_hard.txt  file_task16.txt  

Внесем изменения в файл:

	[centos1@andromeda ~]$ cat file_task16.txt 
	This is test example locate
	
Удалим file_task16.txt:

	[centos1@andromeda ~]$ rm file_task16.txt 
	[centos1@andromeda ~]$ ls
	file_task16_hard.txt 

Проверим что данные сохраненные в удаленном файле ранее, остались в _hard.txt :

	[centos1@andromeda ~]$ cat file_task16_hard.txt 
	This is test example locate

 </details>
 
 </details>
 
 <details><summary> Задания лекций 17-18 ( Partitions and LVM )  </summary>
 
 <details><summary> task1  </summary>
 Добавим еще 1 диск нашей виртуальной машине и проверим что мы его добавили корректно:
	
	
	[centos1@andromeda ~]$ lsblk 
	NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
	sda               8:0    0    6G  0 disk 
	├─sda1            8:1    0    1G  0 part /boot
	└─sda2            8:2    0    5G  0 part 
  	  ├─centos-root 253:0    0  4,4G  0 lvm  /
  	  └─centos-swap 253:1    0  616M  0 lvm  [SWAP]
	sdb               8:16   0    5G  0 disk 
	sr0              11:0    1 1024M  0 rom  
Наглядно видим sdb - это и есть наш новый диск.


Перейдем к созданию портишнов:

	[centos1@andromeda ~]$ sudo fdisk /dev/sdb 
	Welcome to fdisk (util-linux 2.23.2).

	Command (m for help): g   
	Building a new GPT disklabel (GUID: 89D4FAF6-2D87-4BE9-A006-A41CD7974C1C)


	Command (m for help): n
	Partition number (1-128, default 1): 1
	First sector (2048-10485726, default 2048): 
	Last sector, +sectors or +size{K,M,G,T,P} (2048-10485726, default 10485726): +2G
	Created partition 1


	Command (m for help): p

	Disk /dev/sdb: 5368 MB, 5368709120 bytes, 10485760 sectors
	Units = sectors of 1 * 512 = 512 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk label type: gpt
	Disk identifier: 71EB548A-2922-4AB9-B337-9BF6BDA79184


	#         Start          End    Size  Type            Name
 	1         2048      4196351      2G  Linux filesyste

	Command (m for help): n 
	Partition number (2-128, default 2): 2
	First sector (4196352-10485726, default 4196352): 
	Last sector, +sectors or +size{K,M,G,T,P} (4196352-10485726, default 10485726): +512M
	Created partition 2
	
	Command (m for help): t
	Partition number (1,2, default 2): 2
	Partition type (type L to list all types): 19
	
	Changed type of partition 'Linux filesystem' to 'Linux swap'

	Command (m for help): p

	Disk /dev/sdb: 5368 MB, 5368709120 bytes, 10485760 sectors
	Units = sectors of 1 * 512 = 512 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk label type: gpt
	Disk identifier: 71EB548A-2922-4AB9-B337-9BF6BDA79184


	#         Start          End    Size  Type            Name
	1         2048      4196351      2G  Linux filesyste 
 	2      4196352      5244927    512M  Linux swap      

Отключим swap:

	[centos1@andromeda ~]$ sudo swapoff -a

Теперь подключим наш новый swap:
	
	[centos1@andromeda ~]$ sudo mkswap /dev/sdb2
	Setting up swapspace version 1, size = 524284 KiB
	no label, UUID=09e9e5b1-c668-43e3-aaae-f7fab6996e6c

Отформатируем наш 2хгиговый портишн в xfs:

	[centos1@andromeda ~]$ sudo mkfs.xfs /dev/sdb1 
	meta-data=/dev/sdb1              isize=512    agcount=4, agsize=131072 blks
      	   	 =                       sectsz=512   attr=2, projid32bit=1
        	 =                       crc=1        finobt=0, sparse=0
	data     =                       bsize=4096   blocks=524288, imaxpct=25
         	 =                       sunit=0      swidth=0 blks
	naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
	log      =internal log           bsize=4096   blocks=2560, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
	realtime =none                   extsz=4096   blocks=0, rtextents=0


Создадим директорию /backup , затем примонтируем туда наш партишн:


	[centos1@andromeda ~]$ sudo mkdir /backup 
	[centos1@andromeda ~]$ sudo mount /dev/sdb1 /backup/
	[centos1@andromeda ~]$ df -H
	Filesystem               Size  Used Avail Use% Mounted on
	devtmpfs                 508M     0  508M   0% /dev
	tmpfs                    520M     0  520M   0% /dev/shm
	tmpfs                    520M  7,1M  513M   2% /run
	tmpfs                    520M     0  520M   0% /sys/fs/cgroup
	/dev/mapper/centos-root  4,8G  1,7G  3,1G  36% /
	/dev/sda1                1,1G  176M  888M  17% /boot
	tmpfs                    104M     0  104M   0% /run/user/1000
	/dev/sdb1                2,2G   34M  2,2G   2% /backup

В финале запишем изменения для /etc/fstab :

	[centos1@andromeda ~]$ cat /etc/fstab 
	#
	# /etc/fstab
	# Created by anaconda on Fri Feb  5 03:24:11 2021
	#
	# Accessible filesystems, by reference, are maintained under '/dev/disk'
	# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
	#
	/dev/mapper/centos-root /                       xfs     defaults        0 0
	UUID=7c34ecb6-ff4e-4b51-b699-c5b0303aaffd /boot                   xfs     defaults        0 0
	/dev/mapper/centos-swap swap                    swap    defaults        0 0
	/dev/sdb1	/backup		xfs	defaults	1 2
	/dev/sdb2	swap	swap	defaults	0 0
	
Ребут и проверка точки монтирования:

	[centos1@andromeda ~]$ sudo reboot
	[sudo] password for centos1: 
	Connection to 192.168.0.19 closed by remote host.
	Connection to 192.168.0.19 closed.
	outragee@outragee-X220:~$ ssh vm
	centos1@192.168.0.19's password: 
	Last login: Tue Feb 16 11:04:20 2021 from 192.168.0.17
	[centos1@andromeda ~]$ df -H
	Filesystem               Size  Used Avail Use% Mounted on
	devtmpfs                 508M     0  508M   0% /dev
	tmpfs                    520M     0  520M   0% /dev/shm
	tmpfs                    520M  7,1M  513M   2% /run
	tmpfs                    520M     0  520M   0% /sys/fs/cgroup
	/dev/mapper/centos-root  4,8G  1,7G  3,1G  36% /
	/dev/sda1                1,1G  176M  888M  17% /boot
	/dev/sdb1                2,2G   34M  2,2G   2% /backup
	tmpfs                    104M     0  104M   0% /run/user/1000



	
 </details>
 
 
 <details><summary> task2 (LVM)  </summary>
 Как и в 1 таске, создадим партишн в формате "Linux LVM". Убедимся что все сделано верно:
	
	#         Start          End    Size  Type            Name
 	1         2048      4196351      2G  Linux filesyste 
 	2      4196352      5244927    512M  Linux swap      
	3      5244928      9439231      2G  Linux LVM      <-----Это и есть ранее созданный портишн 


Теперь заинициализируем наш физический том. 

	 [centos1@andromeda ~]$ sudo pvcreate /dev/sdb3
   	 Physical volume "/dev/sdb3" successfully created.

	 [centos1@andromeda ~]$ sudo pvs
  	 PV         VG     Fmt  Attr PSize  PFree
  	 /dev/sda2  centos lvm2 a--  <5,00g    0 
  	 /dev/sdb3         lvm2 ---   2,00g 2,00g

Расширим пространство уже имеющейся группы Vg:

	[centos1@andromeda ~]$ sudo vgs
  	VG     #PV #LV #SN Attr   VSize  VFree
  	centos   1   2   0 wz--n- <5,00g    0 
	[centos1@andromeda ~]$ sudo lvs
 	 LV   VG     Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
 	 root centos -wi-ao----   4,39g                                                    
 	 swap centos -wi-ao---- 616,00m   
	
	[centos1@andromeda ~]$ sudo vgextend centos /dev/sdb3 
  	Volume group "centos" successfully extended

	[centos1@andromeda ~]$ sudo vgs
 	 VG     #PV #LV #SN Attr   VSize VFree 
  	centos   2   2   0 wz--n- 6,99g <2,00g
	
Расширим корневое пространство (однако у меня места впритык,поэтому) :
	
	[centos1@andromeda ~]$ sudo lvextend -l +510 /dev/centos/root 
  	Size of logical volume centos/root changed from 4,39 GiB (1125 extents) to <6,39 GiB (1635 extents).
 	 Logical volume centos/root successfully resized.
	[centos1@andromeda ~]$ sudo vgs
 	 VG     #PV #LV #SN Attr   VSize VFree
 	 centos   2   2   0 wz--n- 6,99g 4,00m

Ребут и проверка:

	[centos1@andromeda ~]$ sudo reboot
	Connection to 192.168.0.15 closed by remote host.
	Connection to 192.168.0.15 closed.
	outragee@outragee-X220:~$ ssh centos1@192.168.0.15
	Last login: Sun Feb 28 04:45:40 2021 from 192.168.0.13
	[centos1@andromeda ~]$ sudo vgs
	[sudo] password for centos1: 
  	VG     #PV #LV #SN Attr   VSize VFree
  	centos   2   2   0 wz--n- 6,99g 4,00m

	
 </details>
 </details>
 <details><summary>  Задания лекций 19-20 ( Boot and iptables )  </summary>
 Изменим параметр vm.dirty_ratio. Используя утилиту sysctl:
	
	[centos1@andromeda ~]$ sysctl vm.dirty_ratio
	vm.dirty_ratio = 30
	[centos1@andromeda ~]$ sudo sysctl -w vm.dirty_ratio=10 
	vm.dirty_ratio = 10[centos1@andromeda ~]$ sudo sysctl vm.dirty_ratio 
	vm.dirty_ratio = 10

	
	
Изменим параметр vm.dirty_ratio: Используя файл конфигурации sysctl (конфиг файл расположен в /etc/sysctl.conf):
	
Откроем редактором и добавим строку:
	
	[centos1@andromeda ~]$ sudo vim /etc/sysctl.conf 
	vm.dirty_ratio=15
	[centos1@andromeda ~]$ sudo sysctl -p
	vm.dirty_ratio = 15

Firewalld and Iptables:
Создадим зону Epam на интерфейсе enp0s3, в качестве сервиса запустим только ssh ,а в качестве источника укажем мою подсеть.

	[centos1@andromeda ~]$ sudo firewall-cmd --permanent --new-zone=epam
	success
	[centos1@andromeda ~]$ sudo firewall-cmd --set-default-zone="epam"
	success
	[centos1@andromeda ~]$ sudo firewall-cmd --add-service=ssh --zone=epam
	success
	[centos1@andromeda ~]$ sudo firewall-cmd --list-services --zone=epam
	ssh
	[centos1@andromeda ~]$ sudo firewall-cmd --permanent --zone=epam --add-source=192.168.0.1/24
	success
 	[centos1@andromeda ~]$ sudo  firewall-cmd --permanent --zone=epam --add-interface=enp0s3
	The interface is under control of NetworkManager, setting zone to 'epam'.
	success
	[centos1@andromeda ~]$ sudo firewall-cmd --permanent --zone=epam --list-sources 
	192.168.0.16/24

Выключим firewalld и настроим iptables:

	[centos1@andromeda ~]$ sudo yum install iptables-services
	[centos1@andromeda ~]$ sudo systemctl enable iptables
	[centos1@andromeda ~]$ sudo systemctl start iptables
	[centos1@andromeda ~]$ sudo systemctl disable firewalld
	[centos1@andromeda ~]$ sudo systemctl mask firewalld
!!! На данном этапе у меня имеется уже ранее сконфигурированный предварительно файл iptables.sh , положим его в /etc/  , затем сделаем исполняемым и выполним. 
Отредактируем наш файл и разрешим доступ к ssh из моей подсети только.
	
	iptables -A INPUT -s 192.168.0.16/24 -m state --state NEW -p tcp --dport 22 -j ACCEPT
	iptables -A INPUT -s 192.168.0.15/24 -m state --state NEW -p tcp --dport 22 -j ACCEPT

Посмотрим на правила:

	[centos1@andromeda etc]$ sudo iptables -L -v -n
	Chain INPUT (policy DROP 16 packets, 4160 bytes)
 	pkts bytes target     prot opt in     out     source               destination         
   	0     0 ACCEPT     all  --  lo     *       0.0.0.0/0            0.0.0.0/0           
   	0     0 ACCEPT     all  --  eth1   *       0.0.0.0/0            0.0.0.0/0           
    	2   168 ACCEPT     icmp --  *      *       0.0.0.0/0            0.0.0.0/0            icmptype 0
   	0     0 ACCEPT     icmp --  *      *       0.0.0.0/0            0.0.0.0/0            icmptype 3
    	0     0 ACCEPT     icmp --  *      *       0.0.0.0/0            0.0.0.0/0            icmptype 11
    	0     0 ACCEPT     icmp --  *      *       0.0.0.0/0            0.0.0.0/0            icmptype 8
   	83  5955 ACCEPT     all  --  *      *       0.0.0.0/0            0.0.0.0/0            state RELATED,ESTABLISHED
    	0     0 DROP       all  --  *      *       0.0.0.0/0            0.0.0.0/0            state INVALID
    	0     0 DROP       tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp flags:0x3F/0x00
    	0     0 DROP       tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp flags:!0x17/0x02 state NEW
    	0     0 ACCEPT     tcp  --  *      *       192.168.0.0/24       0.0.0.0/0            state NEW tcp dpt:22
    	0     0 ACCEPT     tcp  --  *      *       192.168.0.0/24       0.0.0.0/0            state NEW tcp dpt:22

	Chain FORWARD (policy DROP 0 packets, 0 bytes)
 	pkts bytes target     prot opt in     out     source               destination         
    	0     0 ACCEPT     all  --  *      *       0.0.0.0/0            0.0.0.0/0            state RELATED,ESTABLISHED
    	0     0 DROP       all  --  *      *       0.0.0.0/0            0.0.0.0/0            state INVALID
    	0     0 ACCEPT     all  --  eth1   enp0s3  0.0.0.0/0            0.0.0.0/0           
    	0     0 REJECT     all  --  enp0s3 eth1    0.0.0.0/0            0.0.0.0/0            reject-with icmp-port-unreachable

	Chain OUTPUT (policy DROP 0 packets, 0 bytes)
 	pkts bytes target     prot opt in     out     source               destination         
    	0     0 ACCEPT     all  --  *      lo      0.0.0.0/0            0.0.0.0/0           
    	0     0 ACCEPT     all  --  *      eth1    0.0.0.0/0            0.0.0.0/0           
   	51 11125 ACCEPT     all  --  *      enp0s3  0.0.0.0/0            0.0.0.0/0           
    	0     0 ACCEPT     all  --  *      *       0.0.0.0/0            0.0.0.0/0            state RELATED,ESTABLISHED
    	0     0 DROP       tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp flags:!0x17/0x02 state NEW

	
 </details>
 </details>
 </details>
