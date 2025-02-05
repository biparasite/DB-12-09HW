# Домашнее задание к занятию " `Базы данных в облаке` " - `Сулименков Алексей`

---

## Задание 1

Задание

Создание кластера

1. Перейдите на главную страницу сервиса Managed Service for PostgreSQL.
2. Создайте кластер PostgreSQL со следующими параметрами:

- класс хоста: s2.micro, диск network-ssd любого размера;
- хосты: нужно создать два хоста в двух разных зонах доступности и указать необходимость публичного доступа, то есть публичного IP адреса, для них;
- установите учётную запись для пользователя и базы.

### Ответ

Создание кластера

<details> <summary>Создание кластера</summary>

![cluster-create](https://github.com/biparasite/DB-12-09HW/blob/main/cluster-create.png "cluster-create")

</details>

- Проверьте, что подключение прошло к master-узлу.

```SQL
select case when pg_is_in_recovery() then 'REPLICA' else 'MASTER' end;
```

<details> <summary>Подключение к master</summary>

![connect-master](https://github.com/biparasite/DB-12-09HW/blob/main/connect-master.png "connect-master")

</details>

- Посмотрите количество подключенных реплик:

```SQL
select count(*) from pg_stat_replication;
```

<details> <summary>количество подключенных реплик</summary>

![count -replicas](https://github.com/biparasite/DB-12-09HW/blob/main/count-replicas.png "count -replicas")

</details>

- Проверьте, что подключение прошло к узлу-реплике.

```SQL
select case when pg_is_in_recovery() then 'REPLICA' else 'MASTER' end;
```

<details> <summary>Подключение к replica</summary>

![connect-replica](https://github.com/biparasite/DB-12-09HW/blob/main/connect-replica.png "connect-replica")

</details>

- Для проверки, что механизм репликации данных работает между зонами доступности облака, выполните запрос к таблице, созданной на предыдущем шаге:

```SQL
select * from test_table;
```

<details> <summary>Select</summary>

![select-replica](https://github.com/biparasite/DB-12-09HW/blob/main/select-replica.png "select-replica")

</details>

Мастер

<details> <summary>Master</summary>

![master_all](https://github.com/biparasite/DB-12-09HW/blob/main/master_all.png "master_all")

</details>

Реплика

<details> <summary>Master</summary>

![replica_all](https://github.com/biparasite/DB-12-09HW/blob/main/replica_all.png "replica_all")

</details>

---
