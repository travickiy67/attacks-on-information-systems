# Травицкий Сергей

# Домашнее задание к занятию «Уязвимости и атаки на информационные системы»

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

------

### Задание 1

Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

Просканируйте эту виртуальную машину, используя **nmap**.

Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

Ответьте на следующие вопросы:

- Какие сетевые службы в ней разрешены?
- Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)
  
*Приведите ответ в свободной форме.*  

<details>
<summary>Ответ1</summary>  

- Установленна Metasploitable

**Скрин**

![img](https://github.com/travickiy67/attacks-on-information-systems/blob/main/img/1.1.png)  

- Просканирована:
- `nmap -sV  192.168.0.8`  
- ` sudo nmap -sV -Pn --script vulners 192.168.0.8`    
- `nmap -S  192.168.0.8`  

- Сканирование с помощью скрипта ` sudo nmap -sV -Pn --script vulners 192.168.0.8` показало все уязвимости с сылками на описание и балами риска  

Службы:  
ftp  
ssh  
telnet  
smtp  
domain  
http  
rpcbind  
netbios-ssn  
login  
tcpwrapped  
java-rmi  
bindshell  
nfs  
mysql  
postgresql  
vnc  
irc  
ajp13  

Ссылки с сайта https://sourceforge.net/projects/metasploitable/:  

https://www.exploit-db.com/exploits/17491   

https://www.exploit-db.com/exploits/6122   

https://www.exploit-db.com/exploits/30020   

https://www.exploit-db.com/exploits/31965  

**Скрины, результат сканирования**

![img](https://github.com/travickiy67/attacks-on-information-systems/blob/main/img/1.2.png)  

![img](https://github.com/travickiy67/attacks-on-information-systems/blob/main/img/1.3.png)  

![img](https://github.com/travickiy67/attacks-on-information-systems/blob/main/img/1.4.png)  

</details>

### Задание 2

Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.

Запишите сеансы сканирования в Wireshark.

Ответьте на следующие вопросы:

- Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
- Как отвечает сервер?

*Приведите ответ в свободной форме.*

<details>
<summary>Ответ2</summary>  
 
Режим SYN.  
Эту технику часто называют сканированием с использованием полуотрытых соединений, т.к. вы не открываете полного TCP соединения.   
Вы посылаете SYN пакет, как если бы вы хотели установить реальное соединение и ждете. Ответы SYN/ACK указывают на то, что порт  
прослушивается (открыт), а RST (сброс) на то, что не прослушивается. Если после нескольких запросов не приходит никакого ответа,  
то порт помечается как фильтруемый. Порт также помечается как фильтруемый, если в ответ приходит ICMP сообщение об ошибке недостижимости.  

`sudo nmap -sS 192.168.0.8`

![img](https://github.com/travickiy67/attacks-on-information-systems/blob/main/img/2.1.png)  

![img](https://github.com/travickiy67/attacks-on-information-systems/blob/main/img/2.2.png)  

Режим FIN.  
В этом случае исследуемой системе отправляется пакет FIN. в ответ узел должен отправить пакет RST для всех закрытых портов.  
На открытые порты система игнорирует пакеты и не отправляет ответа. Данный метод срабатывает только для стека протоколов TCP/IP,  
реализованного в системе UNIX.

`sudo nmap -sF 192.168.0.8`

![img](https://github.com/travickiy67/attacks-on-information-systems/blob/main/img/3.1.png)    

![img](https://github.com/travickiy67/attacks-on-information-systems/blob/main/img/3.2.png)   

Xmas.  
При использовании данного метода на исследуемый порт отправляются пакеты FIN, URG и PUSH. в ответ система должна отправить сообщения RST для всех закрытых портов.  

`sudo nmap -sX 192.168.0.8`

![img](https://github.com/travickiy67/attacks-on-information-systems/blob/main/img/4.1.png)  

![img](https://github.com/travickiy67/attacks-on-information-systems/blob/main/img/4.2.png)  

UDP.  
На каждый порт сканируемой машины отправляется UDP-пакет без данных. Этот метод используется для определения, какие UDP-порты на сканируемом  
хосте являются открытыми.Если в ответ было получено ICMP-сообщение "порт недоступен", это означает, что порт закрыт. В противном случае предполагается,  
что сканируемый порт открыт. Этот метод считается ненадежным, В связи с тем, что протокол UDP не гарантирует доставки, точность данного метода очень сильно  
зависит от множества факторов, влияющих на использование системных и сетевых ресурсов, к тому же он очень медленный   

`sudo nmap -sU 192.168.0.8`  
*Очень долгий процес*  

![img](https://github.com/travickiy67/attacks-on-information-systems/blob/main/img/5.1.png)  

![img](https://github.com/travickiy67/attacks-on-information-systems/blob/main/img/5.2.png)  

</details>

