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
 
 Теперь создадим директорию `/etc/cron.every2days/` и файл `echosender` :
 
 `sudo vim /etc/cron.every2days/echosender`
 
 И отредактируем его:

 
    #!/bin/bash
    echo "Hello" > /opt/hello

 В завершении ,проверим имеются ли ошибки если вывод пуст,то их нет:
 
 `anacron -T`
 
 **2.**
 
 
 </details>
 
 </details>
 </details>

