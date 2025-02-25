# Домашнее задание к занятию "`Репликация и масштабирование`" - `Татаринцев Алексей`

### Задание 1

`На лекции рассматривались режимы репликации master-slave, master-master, опишите их различия.`

1. `master-slave часто используется для обеспечения отказоустойчивости приложений.Кроме этого,она позволяет распределить нагрузку на базу`
   `данных между несколькими серверами,или репликами`

2. `Репликацияmaster-masterпозволяет копировать данные с одного сервера на другой. Эта конфигурация добавляет избыточность и повышает эффективность`
    `при обращении к данным.`

### Задание 2

`Поднимаем через  docker compose`

1. `Опираясь на лекцию создаю следующее наполнение в папке mysql-replication`
![1](https://github.com/Foxbeerxxx/rep1/blob/main/img/img1.png)`
2. `Заполняю файл  docker compose.yml и master>init.sql`
3. `В дириктории выполняю docker-compose up -d`
![2](https://github.com/Foxbeerxxx/rep1/blob/main/img/img2.png)`
4. `Подклчасюь к мастер серверу`
```
docker exec -it mysql-master mysql -u root -proot_password
```
![3](https://github.com/Foxbeerxxx/rep1/blob/main/img/img3.png)`
5. `И запрос показать статус`
```
SHOW MASTER STATUS;
```
![4](https://github.com/Foxbeerxxx/rep1/blob/main/img/img4.png)`

6. `Теперь настраиваем Slave, подключаемся к нему`
```
docker exec -it mysql-slave mysql -u root -proot_password
```
7. `И отправляем запрос`
```
CHANGE MASTER TO
    MASTER_HOST='mysql-master',  
    MASTER_USER='repl_user',
    MASTER_PASSWORD='repl_password',
    MASTER_LOG_FILE='binlog.000004', 
    MASTER_LOG_POS=157;             

START SLAVE;

```

![5](https://github.com/Foxbeerxxx/rep1/blob/main/img/img5.png)`

8. `SHOW SLAVE STATUS\G`

![6](https://github.com/Foxbeerxxx/rep1/blob/main/img/img6.png)`


