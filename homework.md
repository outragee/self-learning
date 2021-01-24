## Задачи:

 <details><summary>  Задания лекций 1-2 от 12.01.21 </summary>
  
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


 </details>
 </details>

