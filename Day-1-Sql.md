```sql

-- Start 

create database figma;

create table Users(
    id int auto_increment primary key,
    username varchar(25) unique not null,
    email varchar(25) unique not null ,
    password varchar(25) not null ,
    role enum('designer', 'admin', 'user') default 'user',
    craetedAt timestamp default current_timestamp
);

insert into Users values (default, 'mood-1', 'mood@email.com', 'pass123', 'admin', default);
insert into Users values (default, 'mood-2', 'mood2@email.com', 'pass123', 'designer', default);
insert into Users values (default, 'mood-3', 'mood3@email.com', 'pass123', default, default);
insert into Users values (default, 'mood-4', 'mood4@email.com', 'pass123', default, default);
insert into Users values (default, 'mood-5', 'mood5@email.com', 'pass123', 'designer', default);
update Users set email = "mood@gmail.com" where id = 1;
delete from Users where id = 3;


create table Community_profiles(
    id int auto_increment primary key ,
    user_id int not null ,
    profile_name varchar(25),
    bio text,
    website_url varchar(35) default null,
    x_url varchar(35) default null,
    createdAt timestamp default current_timestamp,
    foreign key (user_id) references Users(id)
);

insert into Community_profiles values (default, 1, 'Mohammed Profile', 'java Developer and designer', default, default, default);

create table Projects (
    id int auto_increment primary key ,
    user_id int not null ,
    project_name varchar(40) not null ,
    description text not null ,
    createdAt timestamp default current_timestamp,
    foreign key (user_id) references Users(id)
);

insert into Projects values (default, 1, 1, 'Create figma ux/ui', 'Create new Ux desgin of figma application', default);


create table Products (
    id int auto_increment primary key ,
    profile_id int not null ,
    product_name varchar(40),
    product_type enum('plugin', 'widget', 'template'),
    description text not null ,
    price decimal(10, 2),
    createdAt timestamp default current_timestamp,
    foreign key (profile_id) references Community_profiles(id)
);

insert into Products values (default, 1, 'Figma UX/UI', 'template', 'Create new Ux desgin of figma application', 80.99,  default);


create table Files (
    id int auto_increment primary key ,
    project_id int not null ,
    file_name varchar(40),
    file_type varchar(40),
    file_size int,
    createdAt timestamp default current_timestamp,
    foreign key (project_id) references Projects(id)
);

insert into Files values (default, 1, default, default, 1024,  default);
alter table Files alter column file_name set default 'Untitled';
alter table Files alter column file_type set default 'fig';


create table Product_files (
    id int auto_increment primary key ,
    product_id int not null ,
    file_name varchar(40) default 'Untitled',
    file_type varchar(40) default 'fig',
    file_size int,
    createdAt timestamp default current_timestamp,
    foreign key (product_id) references Products(id)
);

insert into Product_files values (default, 1, 'plugin.zip', 'zip', 1024, default);

create table Product_comments (
    id int auto_increment primary key ,
    content text not null ,
    product_id int not null ,
    user_id int not null ,
    createdAt timestamp default current_timestamp,
    foreign key (product_id) references Products(id),
    foreign key (user_id) references Users(id)
);
insert into Product_comments values (default, 'good plugin and useful', 1, 1, default);

create table Purchases(
    id int auto_increment primary key ,
    product_id int not null ,
    user_id int not null ,
    purchase_date timestamp default current_timestamp,
    amount decimal(10, 2),
    foreign key (product_id) references Products(id),
    foreign key (user_id) references Users(id)
);
insert into  Purchases values (default, 1, 1, default, 80.99);


create table Transactions (
    id int auto_increment primary key ,
    user_id int not null ,
    amount decimal(10, 2),
    transaction_date timestamp default current_timestamp,
    transaction_type enum ('purchase', 'sale'),
    foreign key (user_id) references Users(id)
);

insert into Transactions values (default, 1, 80.99, default, 'purchase');

-- END

```