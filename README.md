# Домашнее задание к занятию 10.5 "`Балансировка нагрузки. HAProxy/Nginx`" - `Емельянов Михаил`

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

Желаем успехов в выполнении домашнего задания!

---

### Задание 1

Что такое балансировка нагрузки и зачем она нужна? 

*Приведите ответ в свободной форме.*

#### ОТВЕТ:

Балансировка нагрузки распределяет нагрузку между несколькими вычислительными ресурсами, такими как компьютеры, компьютерные кластеры, сети, центральные процессоры или диски.
Цель балансировки нагрузки — оптимизация использования ресурсов, максимизация пропускной способности, уменьшение времени отклика и предотвращение перегрузки какого-либо одного ресурса.
Использование нескольких компонентов балансировки нагрузки вместо одного компонента может повысить надежность и доступность за счет резервирования.
Балансировка нагрузки предполагает обычно наличие специального программного обеспечения или аппаратных средств, таких как многоуровневый коммутатор или система доменных имен, как серверный процесс.

Балансировка нагрузки отличается от физического соединения тем, что балансировка нагрузки делит трафик между сетевыми интерфейсами на сетевой сокет (модель OSI уровень 4) основе, в то время как соединение канала предполагает разделение трафика между физическими интерфейсами на более низком уровне, либо в пакет (модель OSI уровень 3) или по каналу связи (модель OSI уровень 2).

---

### Задание 2

Чем отличаются алгоритмы балансировки Round Robin и Weighted Round Robin? В каких случаях каждый из них лучше применять? 

*Приведите ответ в свободной форме.*

#### ОТВЕТ:

*Round Robin* или алгоритм кругового обслуживания, представляет собой перебор по круговому циклу: первый запрос передаётся одному серверу, затем следующий запрос передаётся другому и так до достижения последнего сервера, а затем всё начинается сначала.

Самой распространёной имплементацией этого алгоритма является, конечно же, метод балансировки Round Robin DNS.
Как известно, любой DNS-сервер хранит пару «имя хоста — IP-адрес» для каждой машины в определённом домене.
С каждым именем из списка можно ассоциировать несколько IP-адресов.
DNS-сервер проходит по всем записям таблицы и отдаёт на каждый новый запрос следующий IP-адрес: например, на первый запрос — xxx.xxx.xxx.2, на второй — ххх.ххх.ххх.3, и так далее.
В результате все серверы в кластере получают одинаковое количество запросов.
Это круто работает, когда запросы по весу одинаковые...

*Weighted Round Robin* — усовершенствованная версия алгоритма Round Robin.

Суть усовершенствований заключается в следующем: каждому серверу присваивается весовой коэффициент в соответствии с его производительностью и мощностью.
Это помогает распределять нагрузку более гибко: серверы с большим весом обрабатывают больше запросов.
Хорошо, когда есть один мощный сервер и, например, два не очень мощных. Мы отдаем 2/3 нагрузки мощному и по 1/6 каждому оставшемуся...
---

### Задание 3

Установите и запустите Haproxy.

*Приведите скриншот systemctl status haproxy, где будет видно, что Haproxy запущен.*

#### ОТВЕТ:

![Скриншот-1](https://github.com/Monooks/10-05_NetoHW/blob/main/img/10.05_1.png)
---

### Задание 4

Установите и запустите Nginx.

*Приведите скриншот systemctl status nginx, где будет видно, что Nginx запущен.*

#### ОТВЕТ:

![Скриншот-2](https://github.com/Monooks/10-05_NetoHW/blob/main/img/10.05_2.png)
---

### Задание 5

Настройте Nginx на виртуальной машине таким образом, чтобы при запросе:

`curl http://localhost:8088/ping`

он возвращал в ответе строчку: 

"nginx is configured correctly".

*Приведите конфигурации настроенного Nginx сервиса и скриншот результата выполнения команды curl http://localhost:8088/ping.*

#### ОТВЕТ:

![Скриншот-3](https://github.com/Monooks/10-05_NetoHW/blob/main/img/10.05_3.png)
![Скриншот-4](https://github.com/Monooks/10-05_NetoHW/blob/main/img/10.05_4.png)
---

## Задания со звёздочкой*

Эти задания дополнительные. Их выполнять не обязательно. На зачёт это не повлияет. Вы можете их выполнить, если хотите глубже разобраться в материале.

---

### Задание 6*

Настройте Haproxy таким образом, чтобы при ответе на запрос:

`curl http://localhost:8080/`

он проксировал его в Nginx на порту 8088, который был настроен в задании 5 и возвращал от него ответ: 

"nginx is configured correctly". 

*Приведите конфигурации настроенного Haproxy и скриншоты результата выполнения команды curl http://localhost:8080/.*
