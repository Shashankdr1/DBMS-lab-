Experiment 1:
create table PUBLISHER (Name varchar(20) primary key,Phone bigint, Address varchar(20)) ;

create table BOOK (Book_id integer primary key, Title varchar(20), Pub_Year date, Publisher_Name 
varchar(20),Foreign key(Publisher_Name) references Publisher(Name) on delete cascade);

create table BOOK_AUTHORS (Author_Name varchar(20), Book_id integer,foreign key(Book_id) 
references Book(Book_id) on delete cascade, primary key(Book_id, Author_Name));
create table LIBRARY_BRANCH (Branch_id integer primary key, Branch_Name varchar(20), Address 
varchar(20));

create table BOOK_COPIES (No_of_Copies integer, Book_id integer,foreign key(Book_id) references 
Book(Book_id) on delete cascade, Branch_id integer,foreign key(Branch_id) references 
Library_Branch(Branch_id) on delete cascade, Primary key(Book_id,Branch_id));
create table CARD(Card_no integer primary key);

create table BOOK_LENDING (DATE_OUT date, DUE_DATE date, BOOK_ID integer,foreign 
key(book_id) references Book(Book_id) on delete cascade, Branch_id integer,foreign key(Branch_id) 
references Library_Branch(Branch_id) on delete cascade, Card_no integer, foreign key(Card_no) 
references Card(Card_no) on delete cascade, primary key(Book_id, Branch_id, card_no));

INSERT INTO PUBLISHER VALUES ('MCGRAW-HILL', 9989076587, 'BANGALORE');
INSERT INTO PUBLISHER VALUES ('PEARSON', 9889076565, 'NEWDELHI');
INSERT INTO PUBLISHER VALUES ('RANDOM HOUSE', 7455679345, 'HYDRABAD');
INSERT INTO PUBLISHER VALUES ('HACHETTE LIVRE', 8970862340, 'CHENAI');
INSERT INTO PUBLISHER VALUES ('GRUPO PLANETA', 7756120238, 'BANGALORE');

INSERT INTO BOOK VALUES (1,'DBMS','2017-01-01','MCGRAW-HILL');
INSERT INTO BOOK VALUES (2,'ADBMS','2016-06-22', 'MCGRAW-HILL');
INSERT INTO BOOK VALUES (3,'CN','2016-09-24', 'PEARSON');
INSERT INTO BOOK VALUES (4,'CG','2015-09-13', 'GRUPO PLANETA');
INSERT INTO BOOK VALUES (5,'OS','2016-05-09', 'PEARSON');

INSERT INTO BOOK_AUTHORS VALUES ('NAVATHE', 1);
INSERT INTO BOOK_AUTHORS VALUES ('NAVATHE', 2);
INSERT INTO BOOK_AUTHORS VALUES ('TANENBAUM', 3);
INSERT INTO BOOK_AUTHORS VALUES ('EDWARD ANGEL', 4);
INSERT INTO BOOK_AUTHORS VALUES ('GALVIN', 5);

INSERT INTO LIBRARY_BRANCH VALUES (10,'RR NAGAR','BANGALORE');
INSERT INTO LIBRARY_BRANCH VALUES (11,'RNSIT','BANGALORE');
INSERT INTO LIBRARY_BRANCH VALUES (12,'RAJAJI NAGAR', 'BANGALORE');
INSERT INTO LIBRARY_BRANCH VALUES (13,'NITTE','MANGALORE');
INSERT INTO LIBRARY_BRANCH VALUES (14,'MANIPAL','UDUPI');

INSERT INTO BOOK_COPIES VALUES (10, 1, 10);
INSERT INTO BOOK_COPIES VALUES (5, 1, 11);
INSERT INTO BOOK_COPIES VALUES (2, 2, 12);
INSERT INTO BOOK_COPIES VALUES (5, 2, 13);
INSERT INTO BOOK_COPIES VALUES (7, 3, 14);
INSERT INTO BOOK_COPIES VALUES (1, 5, 10);
INSERT INTO BOOK_COPIES VALUES (3, 4, 11);

INSERT INTO CARD VALUES (100);
INSERT INTO CARD VALUES (101);
INSERT INTO CARD VALUES (102);
INSERT INTO CARD VALUES (103);
INSERT INTO CARD VALUES (104);

INSERT INTO BOOK_LENDING VALUES ('2017-01-01','2017-06-01', 1, 10, 101);
INSERT INTO BOOK_LENDING VALUES ('2017-01-11','2017-03-11', 3, 14, 101);
INSERT INTO BOOK_LENDING VALUES ('2017-02-21','2017-04-21', 2, 13, 101);
INSERT INTO BOOK_LENDING VALUES ('2017-03-15','2017-07-15', 4, 11, 101);
INSERT INTO BOOK_LENDING VALUES ('2017-04-12','2017-05-12', 1, 11, 104);

Experiment 2:
create table SALESMAN (Salesman_id integer primary key, Name varchar(20), City varchar(20), 
Commission varchar(4));

create table CUSTOMER1 (Customer_id integer primary key, Cust_Name varchar(20), City 
varchar(20), Grade integer, Salesman_id integer, foreign key(Salesman_id) references 
SALESMAN(salesman_id) on delete cascade);

create table ORDERS (Ord_No integer primary key, Purchase_Amt integer, Ord_Date date, 
Customer_id integer, foreign key(Customer_id) references CUSTOMER1(customer_id) on delete 
cascade, Salesman_id integer, foreign key(Salesman_id) references SALESMAN(salesman_id) on 
delete cascade);

INSERT INTO SALESMAN VALUES (1000, 'JOHN','BANGALORE','25 %');
INSERT INTO SALESMAN VALUES (2000, 'RAVI','BANGALORE','20 %');
INSERT INTO SALESMAN VALUES (3000, 'KUMAR','MYSORE','15 %');
INSERT INTO SALESMAN VALUES (4000, 'SMITH','DELHI','30 %');
INSERT INTO SALESMAN VALUES (5000, 'HARSHA','HYDERABAD','15 %');

INSERT INTO CUSTOMER1 VALUES (10, 'PREETHI','BANGALORE', 100, 1000);
INSERT INTO CUSTOMER1 VALUES (11, 'VIVEK','MANGALORE', 300, 1000);
INSERT INTO CUSTOMER1 VALUES (12, 'BHASKAR','CHENNAI', 400, 2000);
INSERT INTO CUSTOMER1 VALUES (13, 'CHETHAN','BANGALORE', 200, 2000);
INSERT INTO CUSTOMER1 VALUES (14, 'MAMATHA','BANGALORE', 400, 3000);

INSERT INTO ORDERS VALUES (50, 5000, '2017-05-04', 10, 1000);
INSERT INTO ORDERS VALUES (51, 450, '2017-01-20', 10, 2000);
INSERT INTO ORDERS VALUES (52, 1000, '2017-02-24', 13, 2000);
INSERT INTO ORDERS VALUES (53, 3500, '2017-04-13', 14, 3000);
INSERT INTO ORDERS VALUES (54, 550, '2017-03-09', 12, 2000);

Experiment 3:
create table ACTOR(act_id integer primary key, act_name varchar(10), act_gender varchar(1));
create table DIRECTOR(dir_id integer primary key, dir_name varchar(20), dir_phone bigint);
create table MOVIES(mov_id integer primary key, mov_title varchar(20), mov_year integer, 
mov_lang varchar(10), dir_id integer, foreign key(dir_id) references DIRECTOR(dir_id) on delete 
cascade);

create table MOVIE_CAST(act_id integer, foreign key(act_id) references ACTOR(act_id) on delete 
cascade, mov_id integer, foreign key(mov_id) references MOVIES(mov_id) on delete cascade, role 
varchar(10), primary key(act_id,mov_id));

create table RATING(mov_id integer, foreign key(mov_id) references MOVIES(mov_id) on delete 
cascade, rev_stars integer, primary key(mov_id,rev_stars));

INSERT INTO ACTOR VALUES (301,'ANUSHKA','F');
INSERT INTO ACTOR VALUES (302,'PRABHAS','M');
INSERT INTO ACTOR VALUES (303,'PUNITH','M');
INSERT INTO ACTOR VALUES (304,'JERMY','M');

INSERT INTO DIRECTOR VALUES (60,'RAJAMOULI', 8751611001);
INSERT INTO DIRECTOR VALUES (61,'HITCHCOCK', 7766138911);
INSERT INTO DIRECTOR VALUES (62,'FARAN', 9986776531);
INSERT INTO DIRECTOR VALUES (63,'STEVEN SPIELBERG', 8989776530);

INSERT INTO MOVIES VALUES (1001,'BAHUBALI-2', 2017, 'TELAGU', 60);
INSERT INTO MOVIES VALUES (1002,'BAHUBALI-1', 2015, 'TELAGU', 60);
INSERT INTO MOVIES VALUES (1003,'AKASH', 2008, 'KANNADA', 61);
INSERT INTO MOVIES VALUES (1004,'WAR HORSE', 2011, 'ENGLISH', 63);

INSERT INTO MOVIE_CAST VALUES (301, 1002, 'HEROINE');
INSERT INTO MOVIE_CAST VALUES (301, 1001, 'HEROINE');
INSERT INTO MOVIE_CAST VALUES (303, 1003, 'HERO');
INSERT INTO MOVIE_CAST VALUES (303, 1002, 'GUEST');
INSERT INTO MOVIE_CAST VALUES (304, 1004, 'HERO');

INSERT INTO RATING VALUES (1001, 4);
INSERT INTO RATING VALUES (1002, 2);
INSERT INTO RATING VALUES (1003, 5);
INSERT INTO RATING VALUES (1004, 4);
