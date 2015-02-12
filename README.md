# SQL
TABLES.sql /* Keira tabele za bazu fakulteta*/

/* Kreira student tabelu*/

  create table if not exists Students (
	student_id integer primary key autoincrement,
	name varchar(15) not null,
	surname varcahr(15) not null,
	study_year smallint default 1);

/* Kreira tabelu za profesore*/
create table if not exists Lecturers (
	id integer primary key autoincrement,
	name varchar(15) not null,
	surname varcahr(15) not null,
	salary integer default 1000);

/* Kreira tabelu za predmete*/
create	table if not exists Courses (
	code varchar(6) primary key,
	name varchar(15) not null,
	num_student smallint default 15);

/* Kreira relacijsku tabelu studenta i predmeta*/
create table if not exists course_taken (
	student_id integer ,
	course_code varchar(6) ,
	grade smallint,
	foreign key (student_id) references	Students,
	foreign key (course_code) references Courses,
	primary key (student_id,course_code));

/* Kreira relacijsku tabelu profesora i predmeta*/
create table if not exists course_taught (
	lecturer_id integer ,
	course_code varchar(6),
	foreign key (lecturer_id) references Lecturerson update cascade on delete cascade,
	foreign key (course_code) references Courses,
	primary key (lecturer_id,course_code)
	);
	
SEED.sql /* Unos podataka*/

insert into Students values(?,'Haris','Arifovic',2);
insert into Students values(?,'Selma','Tabakovic',1);
insert into Students values(?,'Superman','Batman',3);
insert into Students values(?,'Vega','Sagat',2);

insert into	Lecturers values(?,"Get",'Right',3500);
insert into	Lecturers values(?,"OLOF",'MEISTER',3000);
insert into	Lecturers values(?,"J",'W',2500);
insert into	Lecturers values(?,"Hiko",'Spencer',1500);

insert into Courses values('CS101', "Intro to Java", 20);
insert into Courses values('CS202', "Database Design", 5);
insert into Courses values('NS101', "Chemistry", 15);

insert into course_taken values (1,'CS202',4);
insert into course_taken values (1,'NS101',3);
insert into course_taken values (2,'CS101',5);
insert into course_taken values (2,'NS101',5);
insert into course_taken values (3,'CS202',5);
insert into course_taken values (3,'CS101',2);

insert into course_taught values(1, 'CS101');
insert into course_taught values(2, 'CS202');
insert into course_taught values(3, 'NS101');

QUERY.sql /* Upiti*/

select name as Ime, surname as Prezime, study_year as Godina 
from students
where Godina >2;
select count (name) as BrojStudenata from students;
select avg(salary) as ProsjecnaPlata from lecturers;
select sum(salary) as UkupnaPlata from	lecturers;
select sum(salary) as UkupnaPlata, avg (salary) as ProsjecnaPlata from lecturers;
select name,salary from lecturers order by salary DESC;
select max(salary) as Najveca, min(salary) as Najmanja from lecturers;
select courses.name as cn, lecturers.name as ln from courses
inner join course_taught on courses.code = course_taught.course_code
inner join lecturers on course_taught.lecturer_id = lecturers.id;
