# Users API (Rust, Postgres, Docker, Docker Compose)

## Rust 🦀 CRUD Rest API - Rust, Postgres, Docker, Docker Compose

[rust-crud-api](https://www.youtube.com/watch?v=vhNoiBOuW94&list=PLPoSdR46FgI4K36elsmeoUynDUXhjvtEn&index=3)




## Errors and snippets

clear
docker ps -a
# should be empth; else use docker system prune or container prune

docker compose up -d db  # start the db container, detached

# Error starting userland proxy: listen tcp4 0.0.0.0:5432: bind: address already in use
# system postgres already running; 
# find it and kill by pid
sudo lsof -i :5432
sudo kill 93266

#try again
docker compose up -d db

#inspect the db... interactive terminal, into db process, run psql prompt w default pg user
docker exec -it db psql -U postgres

postgres=# \dt
Did not find any relations.

# table will be created on first run

#NEW terminal: build the app
docker compose build

#once successful, then run the rustapp
docker compose up rustapp

#test all good
docker ps -a  # should be 2 services, rustapp and db
# in the docker exec pg...
postgres=# \dt
         List of relations
 Schema | Name  | Type  |  Owner   
--------+-------+-------+----------
 public | users | table | postgres
(1 row)
postgres=# select * from users;
 id | name | email 
----+------+-------
(0 rows)
# table created; still empty tho

# POSTMAN (web.postman.co)  ...sign in w google
GET http://localhost/users
> []
POST http://localhost/user {"name":"aaa","email":"aaa.mail"}
> user created
...etc
