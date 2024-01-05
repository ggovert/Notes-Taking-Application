# Notes Taking Application
This application was created so it became easier for students in the same class to create notes and even upload their assignment

## Table of Contents
* [Problem Statement and Overview](#problem-statement-and-overview)
* [Tools Used](#tools-used)
* [Creating the Database](#creating-the-database)
* [Creating the Application using Oracle APEX](#creating-the-application-using-oracle-apex)
* [The Application](#the-application)
* [Future Improvement](future-improvement)


## Problem Statement and Overview: 
As a student, we usually create notes to better understand our subject. But sometimes we could miss our class and miss the notes that might be pivotal for our exams. Because of this, we usually ask our friends if they could lend us their notes so we will be not left behind. Wouldn't it be better if we had a centralized note-taking application that can make all of these processes easier, we can easily search for the course and find all of the notes that our classmates have created. From this problem, then I decided to create these note-taking application, so it became easier for students in the same class to create and share notes  and even upload their assignments. 

## Tools Used:
- Tools: Oracle APEX
- Programming Language: Oracle SQL

## Creating the Database:
Before creating the application, it is really important to create the database of the application and define the field of each table. 

  1. We listed which table and all columns we will need. After that, we will do normalization which includes 1NF (First Normal Form), 2NF(Second Normal Form), 3NF(Third Normal Form), we also define the key attributes of the table which are primary key and foreign key. All of these steps are important to reduce data redundancy and improve data integrity.
  * 1NF: Eliminate duplicate columns and make sure each column hold a single value.
  * 2NF: Remove partial dependencies where a non-key attribute depends on only part of the primary key.
  * 3NF: We make sure that no non-key attribute is dependent on another non-key attribute.
 
      
  2. Create an ERD (Entity Relationship Diagram) to give us a visual representation and a clear understanding of how data entities relate to each other. In this stage, we define the relationship between tables whether it is one-to-many relationship or many-to-one relationship. We have to make sure that we don't have many-to-many relationships to avoid data redundancy and ambiguity. 

![image](https://github.com/ggovert/Notes-Taking-Application/assets/111510965/cce4fabd-2b22-4b97-9594-169e170be4f1)


  3. Now we create the database script that we will use to input it on Oracle APEX
      Here is the script that I used to create the database using the oracle sql+ syntax. This script includes  script to create the table, create the sequence, and script to insert the values to the table. You can download the script [here](https://github.com/ggovert/Notes-Taking-Application/blob/main/Notes%20Taking%20Database%20Script.docx)
     

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


   
## Creating the Application using Oracle APEX:

Oracle APEX, or Oracle Application Express, is a low-code web application development platform provided by Oracle Corporation. It enables users to quickly create and deploy scalable and secure applications that can be accessed through web browsers.

This application contains 12 pages in total:
#### 1. Home Page
  - A user-friendly homepage featuring quick-access buttons for immediate navigation to desired pages. Additionally, include a left tab that allows users to effortlessly switch between directories and access various pages with ease.
    
    ![image](https://github.com/ggovert/Notes-Taking-Application/assets/111510965/66d2bc9d-585c-452a-91b8-2ed307810599)

#### 2. Students page
  - This page is to input the student data. Other than creating data, we can also edit the existing data using the pencil icon at left side of the table.
  - Things that worth mentioning is that for the 'state' column, there's no need to manually enter the state; we can simply choose from a list of values that has been provided. this list of values is created using shared component > List of Values, where i created a new table that list all of the states in America and refer this as the list of options that the student can choose. Other than using List of Value, we also can use sql to queue the data that we need as the list of options

    ![image](https://github.com/ggovert/Notes-Taking-Application/assets/111510965/b5f4ef9f-a2f6-495c-b836-d401d6173138)
  
#### 3. Student - Class, Notes, & Assignments (Master-Detail)
* This page show us the student info and all the notes and assignments that they have created and submitted
     ![image](https://github.com/ggovert/Notes-Taking-Application/assets/111510965/e1d454dc-b8de-4440-ad55-730ad0b2d69a)

#### 4. Student Schedule (Faceted Search)
* This page informed us about the each student schedule that we can filter by the name of the students, the courses, and professor. This page make it easier to check the classes schedule that they have for the semester
     ![image](https://github.com/ggovert/Notes-Taking-Application/assets/111510965/8c3dd2b8-c2f5-4fe5-959f-05b4ed214706)

     

#### 5. Professors
* This page is to input the professor data. For the state column, it will use list of values as well, the as the student page
![image](https://github.com/ggovert/Notes-Taking-Application/assets/111510965/50512125-a0f9-4535-baee-184c7023e19b)


#### 6. Courses
* This page is where the student can input our courses and the books that the courses used. The books ISBN column is a using a drop down list based on the column of books pages, because this ISBN column is a foreign key.

![image](https://github.com/ggovert/Notes-Taking-Application/assets/111510965/afb2f7f9-e7b0-409a-9f31-37669be4fe5c)


#### 7. Books
* This page is where the student input and check information about the books ISBN, name, and the publisher. We have to input the ISBN value when we want to create a new data of the books, because the ISBN is the primary key of the BOOKS table.

![image](https://github.com/ggovert/Notes-Taking-Application/assets/111510965/8f14411c-20cc-49b5-898b-36634355a51b)

#### 8. Classes Schedule
* This page is where the student will input their class schedule info.for the form page, there are 2 columns using the drop down list menu which are the Course Type and ProfID column. The student can only choose their option based the data that have been inputed to ProfID column from the professor database and Course Type column from the Courses database.

![image](https://github.com/ggovert/Notes-Taking-Application/assets/111510965/5b849b43-e47e-49f5-8be5-34b4ccde62ee)


#### 9. Assignments
* This page is where student can create and submit their assignment. For the form page, there are 5 columns that has a list down option that was created using shared components (List of Values) and sql which are Course Code, StudentID, Assignment Name, Assignment Week, and Submitted. For Course Code and StudentID column, the only option that they can choose is based from the Student and Classes database because both of these columns are foreign key.

![image](https://github.com/ggovert/Notes-Taking-Application/assets/111510965/8a295dff-95a4-44dd-bbcb-8a209c9f5767)


#### 10. Notes
* This page is where student can create and submit their notes. For the form page, there are 2 columns that has a list down option which are Course Code and Student ID. The only option that they can choose is based from the Student and Classes database because both of this columns are foreign key.

![image](https://github.com/ggovert/Notes-Taking-Application/assets/111510965/27096956-c274-4ad8-b049-abc95cfc2198)


#### 11. Class - Notes& Assignment - (Master Detail)
* This page show us all the the notes and assignment that has been created and submitted for the specific class

![image](https://github.com/ggovert/Notes-Taking-Application/assets/111510965/758d2984-5810-436a-9409-4a3b52fdc558)


#### 12. Courses & Classes - (Master Detail)
* This page show us all the classes schedule for the specific course

![image](https://github.com/ggovert/Notes-Taking-Application/assets/111510965/2082b2d1-aad0-4559-90b6-7459be2a82ec)



## The Application:
To check on the app please feel free to use this account

The application: [Notes-Taking-Application](https://apex.oracle.com/pls/apex/r/ggovert/notes-taking-database-apex/login?session=106027273632026) 

* User: user123@gmail.com
* Pass: ApexACC8080



## Future Improvement:
There are still many things that can be improved. There are several things that i might add in the future to create a better notes taking database application:
1. Create a calendar that can be connected with the dateline of assignment
2. Create an authorization where only the student who created the notes and assignments can edit it.
3. Create a better time table for classes schedule that can be more detailde to the minutes for better accuracy
4. Create a dashboard that can showcase the rate of notes and assignments that being created and submitted
