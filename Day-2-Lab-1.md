```sql

-- Start 

create database store;

create table countries(
    code int primary key ,
    name varchar(20) not null unique ,
    continent_name varchar(20) not null unique
);

insert into countries values(1, 'KSA', 'Asia');
insert into countries values(2, 'EYGPT', 'africa');

update countries set name = 'Japan', continent_name = 'Northeast Asia'  where code = 2;

create table users(
    id int primary key,
    full_name varchar(20) not null,
    email varchar(20) not null unique ,
    gender char(1) check ( gender = 'F' or gender = 'M' ) not null,
    date_of_birth varchar(15),
    country_code int not null unique,
    foreign key (country_code) references countries(code),
    created_at timestamp default current_timestamp
);

insert into users values (1, 'mohammed alomari', 'email@email.com', 'M', '1990-01-01', 1, default);
insert into users values (1, 'mohammed alomari', 'email@email.com', 'M', '1990-01-01', 1, default);



create table orders(
    id int primary key ,
    user_id int not null unique,
    status varchar(6) check ( status = 'start' or status = 'finish') not null ,
    created_at timestamp default current_timestamp,
    foreign key (user_id) references users(id)
);

insert into orders values(1, 1, 'start', default);



create table products(
    id int primary key ,
    name varchar(10) not null,
    price int default 0,
    status varchar(10) check ( status = 'vaild' or status = 'expired') not null ,
    create_at timestamp default current_timestamp
);

insert into products values (1, 'mug', 20, 'vaild', default);


create table order_products(
    order_id int primary key ,
    product_id int unique not null ,
    quantity int default 0,
    foreign key (order_id) references orders(id),
    foreign key (product_id) references products(id)
);

insert into order_products values (1, 1, 10);

-- END

```