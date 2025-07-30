```sql
create database store;

-- -----------------------------

create table countries (
    code int primary key,
    name varchar(20) unique,
    continent_name varchar(20) not null
);

-- -----------------------------

create table users (
    id int primary key,
    full_name varchar(20),
    email varchar(20) unique,
    gender char(1) check (gender='f' or gender='m'),
    date_of_birth varchar(15) not null,
    created_at datetime,
    country_code int,
    foreign key (country_code) references countries(code)
);

-- -----------------------------

create table orders (
    id int primary key,
    user_id int,
    status varchar(6) check (status='start' or status='finish'),
    create_at datetime,
    foreign key (user_id) references users(id)
);

-- -----------------------------

create table products (
    id int primary key,
    name varchar(10) not null,
    price int default 0,
    status varchar(10) check (status='valid' or status='expired'),
    created_at datetime default current_timestamp
);

-- -----------------------------

create table order_products (
    order_id int,
    product_id int,
    quantity int default 0,
    primary key (order_id, product_id),
    foreign key (order_id) references orders(id),
    foreign key (product_id) references products(id)
);

-- -----------------------------

insert into countries (code, name, continent_name) values
(1, 'saudi arabia', 'asia'),
(2, 'usa', 'north america'),
(3, 'germany', 'europe'),
(4, 'japan', 'asia'),
(5, 'brazil', 'south america');

-- -----------------------------

insert into users (id, full_name, email, gender, date_of_birth, created_at, country_code) values
(101, 'hassan yousef', 'hassan@gmail.com', 'm', '2000-01-01', current_timestamp, 1),
(102, 'lina khaled', 'lina@gmail.com', 'f', '1998-05-12', current_timestamp, 2),
(103, 'ali ahmad', 'ali@gmail.com', 'm', '1995-09-25', current_timestamp, 3),
(104, 'sarah ali', 'sarah@gmail.com', 'f', '2001-07-18', current_timestamp, 4),
(105, 'omar nasser', 'omar@gmail.com', 'm', '1999-11-30', current_timestamp, 5);

-- -----------------------------

insert into orders (id, user_id, status, create_at) values
(201, 101, 'start', current_timestamp),
(202, 102, 'finish', current_timestamp),
(203, 103, 'start', current_timestamp),
(204, 104, 'finish', current_timestamp),
(205, 105, 'start', current_timestamp);

-- -----------------------------

insert into products (id, name, price, status) values
(301, 'laptop', 3500, 'valid'),
(302, 'mouse', 50, 'valid'),
(303, 'keyboard', 150, 'valid'),
(304, 'monitor', 700, 'expired'),
(305, 'usb', 30, 'valid');

-- -----------------------------

insert into order_products (order_id, product_id, quantity) values
(201, 301, 1),
(202, 302, 2),
(203, 303, 3),
(204, 304, 1),
(205, 305, 4);

-- -----------------------------

insert into countries (code, name, continent_name)
values (6, 'canada', 'north america');

-- -----------------------------

insert into users (id, full_name, email, gender, date_of_birth, created_at, country_code)
values (106, 'maha salem', 'maha@gmail.com', 'f', '2002-03-14', current_timestamp, 6);

-- -----------------------------

insert into orders (id, user_id, status, create_at)
values (206, 106, 'start', current_timestamp);

-- -----------------------------

insert into products (id, name, price, status)
values (306, 'tablet', 1200, 'valid');

-- -----------------------------

insert into order_products (order_id, product_id, quantity)
values (206, 306, 2);

-- -----------------------------

update countries set name = 'china' where name = 'japan' and code = 4;

-- -----------------------------

update users set full_name = 'hassan y. yousef' where id = 101;

-- -----------------------------

update users set country_code = 4 where id = 105;

-- -----------------------------

update orders set status = 'finish' where id = 201;

-- -----------------------------

update products set name = 'ipad' where name = 'laptop';

-- -----------------------------

update users set country_code = 1 where country_code = 5;

-- -----------------------------

delete from countries where code = 5;

-- -----------------------------

delete from orders where user_id = 105;

-- -----------------------------

delete from users where id = 105;

-- -----------------------------

delete from order_products where order_id = 205;

-- -----------------------------

delete from orders where id = 205;
```
