# Notes Taking Application
This application was created so it became easier for students in the same class to create notes and even upload their assignment

## Problem Statement and Overview: 
As a student, we usually create notes to better understand our subject. But sometimes we could miss our class and miss the notes that might be pivotal for our exams. Because of this, we usually ask our friends if they could lend us their notes so we will be not left behind. Wouldn't it be better if we had a centralized note-taking application that can make all of these processes easier, we can easily search for the course and find all of the notes that our classmates have created. From this problem, then I decided to create these note-taking application, so it became easier for students in the same class to create and share notes  and even upload their assignments. 

## Tools used:
- Oracle APEX

## Creating the database:
Before creating the application, it is really important to create the database of the application and define the field of each table. 

  1. We listed which table and all columns we will need. After that, we will do normalization which includes 1NF (First Normal Form), 2NF(Second Normal Form), 3NF(Third Normal Form), we also define the key attributes of the table which are primary key and foreign key. All of these steps are important to reduce data redundancy and improve data integrity.
    - 1NF: Eliminate duplicate columns and make sure each column hold a single value.
    - 2NF: Remove partial dependencies where a non-key attribute depends on only part of the primary key.
    - 3NF: We make sure that no non-key attribute is dependent on another non-key attribute.
  2. Create an ERD (Entity Relationship Diagram) to give us a visual representation and a clear understanding of how data entities relate to each other. In this stage, we define the relationship between tables whether it is one-to-many relationship or many-to-one relationship. We have to make sure that we don't have many-to-many relationships to avoid data redundancy and ambiguity. 

![image](https://github.com/ggovert/Notes-Taking-Application/assets/111510965/cce4fabd-2b22-4b97-9594-169e170be4f1)


  3. Now we create the database script that we will use to input it on Oracle APEX
      Here is the script that I used to create the database using the oracle sql+ syntax. This script includes  script to create the table.
     
     * Create Table
     ```sql
     
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
    ```

     
     * Create Sequence
     
     ```sql
     
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
```








This application contains 11 pages in total:
1. Home Page
2. Students page
  - Student - Class, Notes, & Assignments (Master-Detail)
  - Student Schedule (Faceted Search)
3. Professors
4. Courses
5. Books
6. Assignments
7. Notes
8. Class - Notes& Assignment - (Master Detail)
9. Courses & Classes - (Master Detail)

