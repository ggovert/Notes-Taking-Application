# Notes Taking Application
This application was created so it became easier for students in the same class to create notes and even upload their assignment

## Table of Contents

## Problem Statement and Overview: 
As a student, we usually create notes to better understand our subject. But sometimes we could miss our class and miss the notes that might be pivotal for our exams. Because of this, we usually ask our friends if they could lend us their notes so we will be not left behind. Wouldn't it be better if we had a centralized note-taking application that can make all of these processes easier, we can easily search for the course and find all of the notes that our classmates have created. From this problem, then I decided to create these note-taking application, so it became easier for students in the same class to create and share notes  and even upload their assignments. 

## Tools used:
- Oracle APEX

## Creating the database:
Before creating the application, it is really important to create the database of the application and define the field of each table. 

  1. We listed which table and all columns we will need. After that, we will do normalization which includes 1NF (First Normal Form), 2NF(Second Normal Form), 3NF(Third Normal Form), we also define the key attributes of the table which are primary key and foreign key. All of these steps are important to reduce data redundancy and improve data integrity.
  * 1NF: Eliminate duplicate columns and make sure each column hold a single value.
  * 2NF: Remove partial dependencies where a non-key attribute depends on only part of the primary key.
  * 3NF: We make sure that no non-key attribute is dependent on another non-key attribute.
 
      
  2. Create an ERD (Entity Relationship Diagram) to give us a visual representation and a clear understanding of how data entities relate to each other. In this stage, we define the relationship between tables whether it is one-to-many relationship or many-to-one relationship. We have to make sure that we don't have many-to-many relationships to avoid data redundancy and ambiguity. 

![image](https://github.com/ggovert/Notes-Taking-Application/assets/111510965/cce4fabd-2b22-4b97-9594-169e170be4f1)


  3. Now we create the database script that we will use to input it on Oracle APEX
      Here is the script that I used to create the database using the oracle sql+ syntax. This script includes  script to create the table, create the sequence, and script to insert the values to the table. You can download the script [here]
     

     ```sql

     --Create Table
     
     CREATE TABLE students (
     student_id varchar2(10),
     first_name varchar2(25) NOT NULL,
     last_name varchar2(25) NOT NULL,
     email varchar2 (255) NOT NULL,
     address varchar2 (255) NOT NULL,
     city varchar2 (50) NOT NULL,
     state char(2) NOT NULL,
     zip number (5,0) NOT NULL,
     year_of_entering number NOT NULL,
     CONSTRAINT student_id_pk PRIMARY KEY (student_id) ,
     CONSTRAINT state_us_ck CHECK (state IN( 'AL', 'AK', 'AZ', 'AR', 'CA', 'CO', 'CT', 'DE', 'FL', 'GA', 'HI', 'ID', 'IL', 'IN', 'IA', 'KS', 'KY', 'LA', 'ME', 'MD', 'MA', 'MI', 'MN', 'MS', 'MO', 'MT', 'NE', 'NV', 'NH', 'NJ', 'NM', 'NY', 'NC', 'ND', 'OH', 'OK', 'OR', 'PA', 'RI', 'SC', 'SD', 'TN', 'TX', 'UT', 'VT', 'VA', 'WA', 'WV', 'WI', 'WY' )));

     
     -- Create Sequence
      CREATE SEQUENCE notes_id_seq
      START WITH 1
      INCREMENT BY 1
      MAXVALUE 100000
      NOCACHE
      NOCYCLE;

      CREATE SEQUENCE assignment_id_seq
      START WITH 1
      INCREMENT BY 1
      MAXVALUE 100000
      NOCACHE
      NOCYCLE;

     -- Inserting Values into the table
     INSERT INTO assignment
      VALUES (
        Assignment_id_seq.nextval, 'COSC-1336-001',
        ‘G2290749’, 'W1: Python Function',
        TO_DATE('2023-10-17', 'YYYY-MM-DD'), 
        TO_DATE('2023-10-17', 'YYYY-MM-DD'), 
        TO_DATE('2023-10-14', 'YYYY-MM-DD'), 
        'YES');
     ```

4. Populate the database with data.
          Because i want to check, whether my data is working or not, i was populating my database with some fake data. I was using chat GPT to get the fake name, address, etc for the data, and edit it using Google spreasheet and after that download it as csv so that i can copy it and put it on Oracle APEX. Recently, i also found out that you can populate the database using python with faker and pandas package. I have also included the code

   


This application contains 12 pages in total:
1. Home Page
2. Students page
  3. Student - Class, Notes, & Assignments (Master-Detail)
  4. Student Schedule (Faceted Search)
5. Professors
6. Courses
7. Books
8. Classes Schedule
9. Assignments
10. Notes
11. Class - Notes& Assignment - (Master Detail)
12. Courses & Classes - (Master Detail)

## The apps:
To check on the app please feel free to use this account
The application: https://apex.oracle.com/pls/apex/r/ggovert/notes-taking-database-apex/login?session=106027273632026 

User: user123@gmail.com
Pass: ApexACC8080



## Future Improvement:
There are still many things that can be improved. There are several things that i might add in the future to create a better notes taking database application:
1. Create a calendar that can be connected with the dateline of assignment
2. Create an authorization where only the student who created the notes and assignments can edit it.
3. 
