
**task 1.**  
**Screenshots p1 and p1_2.**  
code:  
create schema LibraryManagement;  
create table authors (  
author_id int auto_increment primary key,  
author_name varchar(50)  
);  
create table genres (  
genre_id int auto_increment primary key,  
genre_name varchar(50)  
);  
create table books (  
book_id int auto_increment primary key,  
title varchar(50),  
publication_year year,  
author_id int,  
 foreign key (author_id) references authors(author_id),   
 genre_id int,  
 foreign key (genre_id) references genres (genre_id)  
);  
create table users (  
user_id int auto_increment primary key,  
username varchar(50),  
email varchar(50)  
);  
create table borrowed_books (  
borrow_id int auto_increment primary key,  
book_id int,  
foreign key (book_id) references books(book_id),  
user_id int,  
foreign key (user_id) references users(user_id),  
borrow_date date,  
return_date date  
);    
**task 2.**   
**Screenshots p2.1-p2.5**  
Code:  
INSERT INTO authors (author_id, author_name)  
VALUES (1, 'James Lann'),  
 (2, 'Kate Rose'),  
 (3, 'Luis Viru');  
   
 INSERT INTO genres (genre_id, genre_name)  
VALUES (1, 'romance'),  
 (2, 'detective'),  
 (3, 'documentary');  
   
 INSERT INTO books (book_id, title, publication_year, author_id, genre_id)  
VALUES (1, 'Road to life', '1996', 2, 2),  
 (2, 'Heart and Soul', '2017', 1, 1),  
 (3, 'Moon exporation', '2004', 3, 3);  
  
INSERT INTO users (user_id, username, email)  
VALUES (1, 'Mary Pole', 'mary@gmail.com'),  
(2, 'Kevin Flister', 'kfl@gmail.com'),  
(3, 'Steve Stevenson','sssn1@gmail.com'),  
(4, 'Samuel Nilson', 'nson@gmail.com');  

INSERT INTO borrowed_books (borrow_id, book_id, user_id, borrow_date, return_date)  
values (1, 2, 3, '2025-05-03', '2025-06-15'),  
(2, 1, 2, '2025-02-03', '2025-03-15'),  
(3, 3, 1, '2025-03-03', '2025-07-15');  

 **task 3.**    
 Screenshot p3.  
 Code:  
 select * from order_details od  
inner join orders o  
on od.order_id=o.id  
inner join products p  
on od.product_id=p.id  
inner join customers c  
on o.customer_id=c.id  
inner join employees e  
on o.employee_id=e.employee_id  
inner join shippers s  
on o.shipper_id=s.id  
inner join suppliers sp  
on p.supplier_id=sp.id  
inner join categories cg  
on p.category_id=cg.id;  

**task 4.**  
Screenshot p4.  
Code:  
select count(*) from order_details od  
inner join orders o  
on od.order_id=o.id   
inner join products p   
on od.product_id=p.id   
inner join customers c  
on o.customer_id=c.id  
inner join employees e  
on o.employee_id=e.employee_id  
inner join shippers s  
on o.shipper_id=s.id  
inner join suppliers sp  
on p.supplier_id=sp.id  
inner join categories cg  
on p.category_id=cg.id;  

**task 5.**  
Screenshot p5.  
Code:  
select count(*)   
from order_details od  
right join orders o  
on od.order_id=o.id  
left join products p  
on od.product_id=p.id  
right join customers c  
on o.customer_id=c.id  
left join employees e  
on o.employee_id=e.employee_id  
left join shippers s  
on o.shipper_id=s.id  
left join suppliers sp  
on p.supplier_id=sp.id  
left join categories cg  
on p.category_id=cg.id;  
Count rows changes only if I change all INNER to Left or Right. Now I get 535 rows, since in Left join we keep all rows in left table (or right with RIGHT) whereas in INNER only matching rows.  

**task 6.**  
Screenshot p6.  
Code:  
select * from order_details od  
inner join orders o  
on od.order_id=o.id  
inner join products p  
on od.product_id=p.id  
inner join customers c  
on o.customer_id=c.id  
inner join employees e  
on o.employee_id=e.employee_id  
inner join shippers s  
on o.shipper_id=s.id  
inner join suppliers sp  
on p.supplier_id=sp.id  
inner join categories cg  
on p.category_id=cg.id  
where o.employee_id between 4 and 10;  

**task 7.**  
Screenshot p7.    
Code:  
select cg.category_name, count(*) as count_rows, avg(od.quantity) as avg_prods   
from order_details od  
inner join orders o  
on od.order_id=o.id  
inner join products p  
on od.product_id=p.id  
inner join customers c  
on o.customer_id=c.id  
inner join employees e  
on o.employee_id=e.employee_id  
inner join shippers s  
on o.shipper_id=s.id  
inner join suppliers sp  
on p.supplier_id=sp.id  
inner join categories cg  
on p.category_id=cg.id  
group by cg.category_name;  


**task 8.**  
Screenshot p8.    
Code:  
select cg.category_name, count(*) as count_rows, avg(od.quantity) as avg_prods  
from order_details od  
inner join orders o  
on od.order_id=o.id  
inner join products p  
on od.product_id=p.id  
inner join customers c  
on o.customer_id=c.id  
inner join employees e  
on o.employee_id=e.employee_id  
inner join shippers s  
on o.shipper_id=s.id  
inner join suppliers sp  
on p.supplier_id=sp.id  
inner join categories cg  
on p.category_id=cg.id  
group by cg.category_name  
having avg_prods>21;  

**task 9.**  
Screenshot p9.    
Code:  
select cg.category_name, count(*) as count_rows, avg(od.quantity) as avg_prods  
from order_details od  
inner join orders o  
on od.order_id=o.id  
inner join products p  
on od.product_id=p.id  
inner join customers c  
on o.customer_id=c.id  
inner join employees e  
on o.employee_id=e.employee_id  
inner join shippers s  
on o.shipper_id=s.id  
inner join suppliers sp  
on p.supplier_id=sp.id  
inner join categories cg  
on p.category_id=cg.id  
group by cg.category_name  
having avg_prods>21  
order by count_rows desc;  

**task 10.**  
Screenshot p10.    
Code:  
select cg.category_name, count(*) as count_rows, avg(od.quantity) as avg_prods  
from order_details od  
inner join orders o  
on od.order_id=o.id  
inner join products p  
on od.product_id=p.id  
inner join customers c  
on o.customer_id=c.id  
inner join employees e  
on o.employee_id=e.employee_id  
inner join shippers s  
on o.shipper_id=s.id  
inner join suppliers sp  
on p.supplier_id=sp.id  
inner join categories cg  
on p.category_id=cg.id  
group by cg.category_name  
having avg_prods>21  
order by count_rows desc  
limit 4 offset 1;  



