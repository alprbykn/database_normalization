# database_normalization
# database normalization, query optimization, indexing examples just not to lose it

##161180072- Alper Beykan YOLCU
##CENG 316 DATABASE SYSTEMS FINAL
##ANKARA UNIVERCITY REGISTERY CREDIT SYSTEMM
CREATE TABLE students (
    s_id INT PRIMARY KEY,
    s_name VARCHAR(30),
    gender VARCHAR(6),
    gpa     DECIMAL(5,3)
);#IS IS UNNECESSERY TO LINK STUDENTS TO INSTRUCTORS LIKE TEACHES OR LINKING TO COUSE LIKE GETS GRADE FOR THIS EXAMPLES 
#DIFFERENT FROM MY E-R TABLE SO THIS RELATIONSHIPS WILL NOT BE LINKED
CREATE TABLE program(
    s_id INT,
    FOREIGN KEY (s_id) REFERENCES students(s_id) ON DELETE SET NULL,
    course_1 VARCHAR(6),
    course_2 VARCHAR(6),
    course_3 VARCHAR(6),
    course_4 VARCHAR(6)
);
CREATE TABLE instructors (
    i_id INT PRIMARY KEY,
    i_name VARCHAR(30),
    department VARCHAR(6),
    title VARCHAR(10),#max professor
    salary INT
);
CREATE TABLE courses (
    c_id INT PRIMARY KEY,
    must VARCHAR(4),#must or elec
    credits INT,
    akts INT,
    prerequisites VARCHAR(50),
    adoptation VARCHAR(10),
    syllabus LONGTEXT
);
CREATE TABLE course_offerings (
    c_id INT,
    FOREIGN KEY (c_id) REFERENCES courses (c_id) ON DELETE SET NULL,
    semester VARCHAR(6),
    c_year INT,
    section_number INT,
    classroom INT,
    i_id INT,
    FOREIGN KEY (i_id) REFERENCES instructors (i_id) ON DELETE SET NULL
);


CREATE TABLE timings(
    c_id INT,
    FOREIGN KEY (c_id) REFERENCES courses(c_id) ON DELETE SET NULL,
    timing1 VARCHAR(2),
    timing2 VARCHAR(2),
    timing3 VARCHAR(2),
    timing4 VARCHAR(2),
    timing5 VARCHAR(2),
    timing6 VARCHAR(2)
);

DESCRIBE students;
DROP TABLE courses;

INSERT INTO students VALUES(161112341,'tarkan tevetoglu','male','3.8');
INSERT INTO students VALUES(161112342,'serdar ortac','male','3.9');
INSERT INTO students VALUES(161112343,'izzet yildizhan','male','2.6');
INSERT INTO students VALUES(161112344,'sertap erener','female','3.5');
INSERT INTO students VALUES(161112345,'murat boz','male','2.13');
INSERT INTO students VALUES(161112346,'ajdar superstar','male','0.67');
INSERT INTO students VALUES(161112347,'candan ercetin','female','1.88');
INSERT INTO students VALUES(161112348,'mustafa sandal','male','3.1');
INSERT INTO students VALUES(161112349,'asik veysel','male','3.67');
INSERT INTO students VALUES(161112310,'mustafa ceceli','male','2.67');
INSERT INTO students VALUES(161112311,'mustafa sandal','male','1.67');

INSERT INTO instructors VALUES(990000001,'kurtulus kullu','BM','dr','5026');
INSERT INTO instructors VALUES(990000002,'fatos onsoy','BM','idari','4621');
INSERT INTO instructors VALUES(990000003,'refik samet','BM','professor','13026');
INSERT INTO instructors VALUES(990000010,'ahmet hasim','BM','docent','7631');
INSERT INTO instructors VALUES(990000004,'hacer guler','EEE','dr','5026');
INSERT INTO instructors VALUES(990000005,'orhan ozturk','EEE','muhendis','6329');
INSERT INTO instructors VALUES(990000011,'halide goksel','EEE','idari','3321');
INSERT INTO instructors VALUES(990000006,'murat efe','EEE','professor','13026');
INSERT INTO instructors VALUES(990000007,'bulent akay','KM','professor','13026');
INSERT INTO instructors VALUES(990000008,'berna topuz','KM','docent','7631');
INSERT INTO instructors VALUES(990000009,'atilla dincer','KM','dr','5026');

INSERT INTO courses VALUES(01001,'must','4','6',NULL,NULL,'course');
INSERT INTO courses VALUES(01002,'must','3','4',NULL,NULL,'course');
INSERT INTO courses VALUES(01201,'must','2','2',NULL,NULL,'course');
INSERT INTO courses VALUES(01309,'slct','4','6',NULL,NULL,'course');
INSERT INTO courses VALUES(01409,'slct','4','6',01309,NULL,'course');
INSERT INTO courses VALUES(02001,'must','3','4',NULL,NULL,'course');
INSERT INTO courses VALUES(02222,'must','4','6',NULL,NULL,'course');
INSERT INTO courses VALUES(02226,'must','4','6',NULL,NULL,'course');
INSERT INTO courses VALUES(02322,'slct','2','2',02222,NULL,'course');
INSERT INTO courses VALUES(02401,'must','3','3',NULL,NULL,'course');
INSERT INTO courses VALUES(03101,'must','6','6',NULL,NULL,'course');
INSERT INTO courses VALUES(03102,'slct','6','6',NULL,NULL,'course');
INSERT INTO courses VALUES(03201,'must','4','6',03101,NULL,'course');
INSERT INTO courses VALUES(03241,'must','2','4',NULL,NULL,'course');
INSERT INTO courses VALUES(03401,'slct','3','4',NULL,NULL,'course');

INSERT INTO course_offerings VALUES(01001,'summer','2021','1',1,'990000001');
INSERT INTO course_offerings VALUES(01002,'summer','2021','1',2,'990000002');
INSERT INTO course_offerings VALUES(01201,'summer','2021','1',3,'990000003');
INSERT INTO course_offerings VALUES(01309,'summer','2021','1',4,'990000010');
INSERT INTO course_offerings VALUES(01409,'summer','2021','1',4,'990000001');
INSERT INTO course_offerings VALUES(02001,'summer','2021','1',5,'990000010');
INSERT INTO course_offerings VALUES(02222,'summer','2021','1',3,'990000004');
INSERT INTO course_offerings VALUES(02226,'summer','2021','1',3,'990000004');
INSERT INTO course_offerings VALUES(02322,'summer','2021','1',6,'990000005');
INSERT INTO course_offerings VALUES(02401,'summer','2021','1',7,'990000011');
INSERT INTO course_offerings VALUES(03101,'summer','2021','1',8,'990000006');
INSERT INTO course_offerings VALUES(03102,'summer','2021','1',8,'990000006');
INSERT INTO course_offerings VALUES(03201,'summer','2021','1',9,'990000007');
INSERT INTO course_offerings VALUES(03241,'summer','2021','1',1,'990000008');
INSERT INTO course_offerings VALUES(03401,'summer','2021','1',9,'990000009');

INSERT INTO timings VALUES(01001,'x','n','x','n','n','n');
INSERT INTO timings VALUES(01002,'n','x','x','n','x','n');
INSERT INTO timings VALUES(01201,'n','n','n','x','x','n');
INSERT INTO timings VALUES(01309,'n','n','n','x','x','n');
INSERT INTO timings VALUES(01409,'x','n','n','x','x','n');
INSERT INTO timings VALUES(02001,'n','n','n','x','n','x');
INSERT INTO timings VALUES(02222,'x','n','n','x','n','n');
INSERT INTO timings VALUES(02226,'x','n','n','x','n','n');
INSERT INTO timings VALUES(02322,'x','x','n','n','n','n');
INSERT INTO timings VALUES(02401,'x','x','n','n','n','x');
INSERT INTO timings VALUES(03101,'x','x','x','n','n','n');
INSERT INTO timings VALUES(03102,'n','x','n','x','n','n');
INSERT INTO timings VALUES(03201,'n','n','n','n','x','x');
INSERT INTO timings VALUES(03241,'n','n','x','n','n','x');
INSERT INTO timings VALUES(03401,'n','n','x','n','x','n');

INSERT INTO program VALUES(161112341,01001,01002,01201,01309);
INSERT INTO program VALUES(161112342,01002,01201,01309,01409);
INSERT INTO program VALUES(161112343,01001,01202,01309,01409);
INSERT INTO program VALUES(161112344,02001,02222,02226,02322);
INSERT INTO program VALUES(161112345,02001,02222,02322,02401);
INSERT INTO program VALUES(161112346,02001,02226,02322,02401);
INSERT INTO program VALUES(161112347,03101,03102,03201,03241);
INSERT INTO program VALUES(161112348,03101,03201,03241,03401);
INSERT INTO program VALUES(161112349,03101,03102,03241,01309);
INSERT INTO program VALUES(161112310,03101,03201,03241,01309);

SELECT * 
FROM students
where gpa > 3;

UPDATE students
SET s_name = 'turkan soray', gender= 'female'
WHERE s_id = 161112311;

SELECT MAX(gpa)
FROM students;

DELETE FROM students WHERE s_name='turkan soray';

INSERT INTO students VALUES(161112311,'mustafa sandal','male','3.21');
##After there we will be apply some techniques on database and see how
##query time, memery usage, database connection, network traffic and latency 
##
##
##1f normal form requires no dublicates, unique id s and no multivalued variables so,
#the existing tables are satisfies 1f normal form.
##
##

##
##
##2f normal form requires 1f and no partial dependencities
##2f normal form
##
##
CREATE TABLE s_infos
  AS (SELECT s_id, s_name, gpa
      FROM students);
CREATE TABLE s_genders
  AS (SELECT s_id, s_name, gender
      FROM students);

CREATE TABLE i_infos
  AS (SELECT i_id, i_name, department
      FROM instructors);
CREATE TABLE i_salaries
  AS (SELECT i_id, title, salary
      FROM instructors);

CREATE TABLE uni_courses
  AS (SELECT c_id, must, credits, akts, syllabus
      FROM courses);
CREATE TABLE course_instructos
  AS (SELECT i_id, s_name
      FROM students);

##
##
##after there most of the columns are in the 2f and 3f form   
##
##

SELECT * 
FROM s_infos
where gpa > 3;

UPDATE s_infos
SET gpa = 3.12 
WHERE s_id = 161112311;

DELETE FROM s_infos WHERE s_name='turkan soray';

SELECT MAX(gpa)
FROM s_infos;


##
##
##APPLYING INDEXING TO USEFULL TABLES
##
##
ALTER TABLE students
ADD INDEX idx_gpa (gpa);

ALTER TABLE instructors
ADD INDEX idx_dep (department);

select * from uni.students where gpa>1
select i_name from uni.instructors where department='KM';
##
##
##APPLYING QUERY OPTIMIZATIONS
##
##
##query optimization depends on the query
##some query optimizations are 
##selecting field manually instead of using select *,
##avoiding distict keyc
##create joins with inner join instead of where
##limiting results
##etc. this syntax changes will effect to the database query metrics
SELECT * 
FROM s_infos
where gpa > 1;

SELECT s_id, s_name, gpa
FROM s_infos
where gpa > 1;

SELECT s_id, s_name, gpa
FROM s_infos
where gpa > 1
limit 3;

SELECT students.s_id, program.course_1,program.course_2,program.course_3,program.course_4
FROM students, program
where students.s_id=program.s_id;

SELECT students.s_id, program.course_1,program.course_2,program.course_3,program.course_4
FROM students
   INNER JOIN program
   ON students.s_id = program.s_id;
