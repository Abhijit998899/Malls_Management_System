# Mall_Management_System

# THIS IS A PROJECT OF SQL
Mall Management System
Role: Database Designer & Backend Developer
Tech Stack: Oracle, SQL, PL/SQL
# Description
Designed and developed the database architecture for a mall management system. Implemented key features such as shop registration, tenant tracking, maintenance logs, and billing using advanced SQL techniques including joins, views, constraints, and multi-table inserts.

# ER Diagram Basic Flow:
Mall
 │
 ├── Shop
 │    ├── Shop Owner
 │    ├── Mall Employee
 │    ├── Inventory
 │    ├── Sales
 │    ├── Orders
 │          └── Customer Orders
 │                 └── Customer
 │          └── Payment
 │
 ├── Food Mall
 ├── Event
 ├── Maintenance Request
 ├── Parking
 └── Rent Payment

 
# ADD THE DATA FOR PROJECT OF Mall_Management_System
1. mall
create table  mall(mall_id number(10) constraint mall_id_pk primary key ,name varchar(30),location varchar(30),contact_number number(20),total_floors number(10),email varchar(20));

INSERT INTO mall (mall_id, name, location, contact_number, total_floors, email) 
VALUES (1, 'City Mall', 'Latur', 9923456789, 5, 'citymall@example.com'),
       (2, 'Mega Mall', 'Pune', 9823456789, 7, 'megamall@example.com');
       
2. shop
 create table shop(shop_id number(20) constraint shop_id_pk primary key, name varchar(20), cotegory varchar(20),floor_number number(20), owner_name varchar(20), mall_id number(10), constraint mall_id2_fk foreign key (mall_id) references mall(mall_id));

INSERT INTO shop (shop_id, name, category, floor_number, owner_name, mall_id) 
VALUES (1, 'Nike Store', 'Sportswear', 1, 'John Doe', 1),
       (2, 'Apple Store', 'Electronics', 2, 'Jane Smith', 1),
       (3, 'The Coffee Shop', 'Food & Beverage', 3, 'Michael Brown', 2);
       
3. shop_owner
 create table shop_owner(owner_id number(10) constraint owner_id_pk primary key ,name varchar(20),email varchar(20),phone_number number(30),shop_id number(10),constraint shop_id3_fk foreign key(shop_id) references shop(shop_id));

INSERT INTO shop_owner (owner_id, name, email, phone_number, shop_id) 
VALUES (1, 'John Doe', 'john.doe@example.com', 9898989898, 1),
       (2, 'Jane Smith', 'jane.smith@example.com', 9797979797, 2);
       
4. mall_employee
 create table mall_employee(employee_id number(10) constraint employee_id_pk primary key ,name varchar(20),role varchar(20),phone_number number(20),salary number(30),hire_date date,shop_id number(10) , constraint shop_id4_fk foreign key (shop_id) references shop(shop_id));

INSERT INTO mall_employee (employee_id, name, role, phone_number, salary, hire_date, shop_id)
VALUES (1, 'Alice Walker', 'Security', 9001234567, 30000, TO_DATE('2023-01-01', 'YYYY-MM-DD'), 1),
       (2, 'Bob Johnson', 'Manager', 9002345678, 50000, TO_DATE('2022-06-15', 'YYYY-MM-DD'), 2);
5. inventory
 create table Inventory(Inventory_id number(20) constraint Inventory_id_pk primary key ,item_name varchar(20),item_category varchar(20),quantity number(20) ,price number(30),supplier_name varchar(20),shop_id number(10), constraint shop_id5_fk foreign key (shop_id) references shop(shop_id));

INSERT INTO inventory (Inventory_id, item_name, item_category, quantity, price, supplier_name, shop_id) 
VALUES (1, 'Nike Shoes', 'Footwear', 50, 5000, 'Nike Supplier', 1),
       (2, 'iPhone 13', 'Mobile', 30, 70000, 'Apple Supplier', 2);
6. customer
 create table Customer(Customer_id number(10) constraint Customer_id_pk primary key , name varchar(20),email varchar(20),phone_number number(20),address varchar(20));

INSERT INTO customer (Customer_id, name, email, phone_number, address) 
VALUES (1, 'Sarah Miller', 'sarah.miller@example.com', 9888888888, 'Latur, Maharashtra'),
       (2, 'David Lee', 'david.lee@example.com', 9777777777, 'Pune, Maharashtra');
7. orders
 create table orders(order_id number(20) constraint order_id_pk primary key ,order_date date ,total_amount number(20), status varchar(20), shop_id number(10) , constraint shop_id7_fk foreign key (shop_id) references shop(shop_id));

INSERT INTO orders (order_id, order_date, total_amount, status, shop_id) 
VALUES (1, TO_DATE('2025-04-25', 'YYYY-MM-DD'), 10000, 'Completed', 1),
       (2, TO_DATE('2025-04-26', 'YYYY-MM-DD'), 15000, 'Pending', 2);
       
8. customer_orders
 create table Customer_orders(Customer_id number(20),constraints Customer_id8_fk foreign key (Customer_id) references Customer(Customer_id),order_id number(10) ,constraint order_id10_fk foreign key (order_id) references orders(order_id));

INSERT INTO customer_orders (Customer_id, order_id) 
VALUES (1, 1),
       (2, 2);
       
9. payment
 create table Payment(Payment_id number(10) constraint Payment_id_pk primary key ,Payment_date date ,Payment_method varchar(10),Payment_status varchar(20),Payment_amount number(10),transaction_id number(20),order_id number(10),constraint order_id11_fk foreign key (order_id)  references orders(order_id));

INSERT INTO payment (Payment_id, Payment_date, Payment_method, Payment_status, Payment_amount, transaction_id, order_id) 
VALUES (1, TO_DATE('2025-04-25', 'YYYY-MM-DD'), 'Credit Card', 'Completed', 10000, 1234567890, 1),
       (2, TO_DATE('2025-04-26', 'YYYY-MM-DD'), 'Debit Card', 'Pending', 15000, 2345678901, 2);
10. sales
 create table sales(sale_id number(10) constraint sale_id_pk primary key,item_name varchar(20),sale_amount number(20),sale_date date ,shop_id number(10),constraint shop_id12_fk foreign key (shop_id) references shop(shop_id));

INSERT INTO sales (sale_id, item_name, sale_amount, sale_date, shop_id) 
VALUES (1, 'Nike Shoes', 50000, TO_DATE('2025-04-25', 'YYYY-MM-DD'), 1),
       (2, 'iPhone 13', 70000, TO_DATE('2025-04-26', 'YYYY-MM-DD'), 2);
11. food_mall
 create table food_mall(food_id number(10) constraint food_id_id_pk primary key,food_name varchar(20),category varchar(20),rating number(10),mall_id number(10),constraint mall_id14_fk foreign key(mall_id) references mall(mall_id));

INSERT INTO food_mall (food_id, food_name, category, rating, mall_id) 
VALUES (1, 'Burger King', 'Fast Food', 4, 1),
       (2, 'Pizza Hut', 'Italian', 5, 2);
12. event
 create table Event(Event_id number(10) constraint Event_id_pk primary key, event_name varchar(20), satrt_date date ,end_date date ,mall_id number(10),constraint mall_id15_fk foreign key(mall_id) references mall(mall_id));

INSERT INTO event (Event_id, event_name, start_date, end_date, mall_id) 
VALUES (1, 'Summer Sale', TO_DATE('2025-05-01', 'YYYY-MM-DD'), TO_DATE('2025-05-07', 'YYYY-MM-DD'), 1),
       (2, 'Food Festival', TO_DATE('2025-06-10', 'YYYY-MM-DD'), TO_DATE('2025-06-15', 'YYYY-MM-DD'), 2);
13. rent_payment
 create table RentPayment(Payment_id number(10) constraint Payment_id22_pk primary key,amount number(20), payment_date date ,payment_status varchar(20), payment_method varchar(20),shop_id number(10),constraint shop_id95_fk foreign key (shop_id) references shop(shop_id));

INSERT INTO RentPayment (Payment_id, amount, payment_date, payment_status, payment_method, shop_id) 
VALUES (1, 50000, TO_DATE('2025-04-25', 'YYYY-MM-DD'), 'Completed', 'Online', 1),
       (2, 60000, TO_DATE('2025-04-26', 'YYYY-MM-DD'), 'Pending', 'Cash', 2);
14. maintenance_request
 create table MaintenanceRequest(request_id number(10) constraint request_id_pk primary key,submitted_by varchar(20),issue_type varchar(20),status varchar(20),request_date date ,mall_id number(10),constraint mall_id11_fk foreign key(mall_id) references mall(mall_id));

INSERT INTO MaintenanceRequest (request_id, submitted_by, issue_type, status, request_date, mall_id) 
VALUES (1, 'John Doe', 'Electrical', 'Completed', TO_DATE('2025-04-22', 'YYYY-MM-DD'), 1),
       (2, 'Jane Smith', 'Plumbing', 'Pending', TO_DATE('2025-04-23', 'YYYY-MM-DD'), 2);
15. parking
 create table parking (parking_id number(10) constraint parking_id_pk primary key ,floor_level number(10),slot_number number(10),status varchar(10),vehicle_number number(10),payment_status varchar(10),mall_id number(10),constraint mall_id22_fk foreign key(mall_id) references mall(mall_id));

INSERT INTO parking (parking_id, floor_level, slot_number, status, vehicle_number, payment_status, mall_id) 
VALUES (1, 1, 101, 'Available', 12345, 'Paid', 1),
       (2, 2, 202, 'Occupied', 67890, 'Unpaid', 2);
16. security_log
 reate table SecurityLog (log_id number(10) constraint log_id_pk primary key,activity_type varchar(20),location varchar(20),employee_id number(20), constraint employee_id33_fk foreign key (employee_id) references mall_employee(employee_id));

INSERT INTO SecurityLog (log_id, activity_type, location, employee_id) 
VALUES (1, 'Patrol', 'Main Entrance', 1),
       (2, 'Inspection', 'Food Court', 2);
17. feedback
 create table Feedback(Feedback_id number(10) constraint Feedback_id_pk primary key,submitted_by varchar(20),message varchar(30),date_submitted date, reting number(10),Customer_id number(10),constraint Customer_id44_fk foreign key (Customer_id) references Customer(Customer_id));

INSERT INTO feedback (Feedback_id, submitted_by, message, date_submitted, rating, Customer_id) 
VALUES (1, 'Sarah Miller', 'Great shopping experience!', TO_DATE('2025-04-25', 'YYYY-MM-DD'), 5, 1),
       (2, 'David Lee', 'Food court needs improvement.', TO_DATE('2025-04-26', 'YYYY-MM-DD'), 3, 2);

