# API-order-lessons
# Project 2 - Order Lessons

## PROJECT DESCRIPTION

Welcome to our app Order Lessons, a backend project where we offer tutoring services for all types of students, where you can book with different teachers depending on the course and subjects you need. There is the possibility of receiving the classes online or in person.


## TEAM
- [Juan Yoel Betancor Martín](https://github.com/Yoel96 )
- [Alexandra Mejías Herrera](https://github.com/AlexandraMH93)
- [Musa Djiguel Camara](https://github.com/Musadjc)

## TECH
- ![Node.js](https://img.shields.io/badge/Node.js-8CC84B?style=for-the-badge&logo=node.js&logoColor=white) **Node.js**
- ![Express](https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white) **Express**
- ![Sequelize](https://img.shields.io/badge/Sequelize-52B0E7?style=for-the-badge&logo=sequelize&logoColor=white) **Sequelize**
- ![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white) **MySQL**
- ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black) **JavaScript (JS)**
- ![Postman](https://img.shields.io/static/v1?style=for-the-badge&message=Postman&color=FF6C37&logo=Postman&logoColor=FFFFFF&label=) **Postman**
- 

## AUTHORIZATION
- **Administrator Role**: The administrator role will have full access to the backend for configuration and maintenance. This means that he/she can modify functionality, query the database and problems with registration and login.
  
- **Teacher**: The teacher role can enter the subjects and the level of the course he/she teaches and configure the available schedules, as well as cancel appointments and indicate whether they are face-to-face or online and their cost.
  
- **Student**: The student's role, once logged in, can choose the course level, the subjects and the teacher. In addition to booking appointments that are available from all teachers, with the option to cancel and choose whether it is face-to-face or online.

 ## REQUERIMENTS
 - Node.js
 - Database(Change .env-> Dialect with the one you use)


 ## INSTALLATION
To get started with the Order Lessons API, just get into the repo and run:
``` npm i ```

# USAGE

Use .env.example to create .env file with your own settings. To start the api server just run:

``` npm run start```

## DATA STRUCTURE AND MODELS
![Screenshot from 2024-03-08 10-02-23](https://github.com/Yoel96/API-order-lessons/assets/145113052/7e3ee3cb-8d5f-4272-baac-4b04c2213169)


### RELATIONS

### One to one
- Ref: "teacher_info"."user_id" - "users"."id"
- Ref: "teacherStudentFavourite"."teacher_id" - "teacher_info"."id"
  
### One to many
- Ref: "teacher_info"."id" < "timetable"."teacher_id"
- Ref: "classesDate"."timeTable_id" < "timetable"."id"

### Many to one
- Ref: "teacherStudentFavourite"."student_id" > "users"."id"
- Ref: "classesDate"."student_id" > "users"."id"
  
### Many to many
- Ref: "lessonType"."subject_id" > "subjects"."id"
- Ref: "lessonType"."teacher_id" > "teacher_info"."id"
- Ref: "teacher_ratings"."user_id" > "users"."id"
- Ref: "teacher_ratings"."teacher_id" > "teacher_info"."id"

 # Backend Endpoints
 
 Base URL: https://api-order-lessons.onrender.com/api
 
 <details>
<summary>:point_right: Auth Endpoints</summary>

| METHOD | ENDPOINT                  | TOKEN | ROLE         | DESCRIPTION                        | POST PARAMS                | RETURNS                              |
| ------ | ------------------------- | ----- | ------------ | ---------------------------------- | -------------------------- | -------------------------------|
| POST   | /signup                   | NO    | Admin        | Creates an account                 | -                          | { token, rol }                 |
| POST   | /login                    | NO    | Admin        | Logs in with corresponding account | -                          | { token, rol }                 |
| POST   | /signup                   | NO    | Teacher      | Creates an account                 | -                          | { token, rol }                 |
| POST   | /login                    | NO    | Teacher      | Logs in with corresponding account | -                          | { token, rol }                 |
| POST   | /signup                   | NO    | Student      | Creates an account                 | -                          | { token, rol }                 |
| POST   | /login                    | NO    | Student      | Logs in with corresponding account | -                          | { token, rol }                 |
</details>

<details>
<summary>:point_right: Student Classdates </summary>

| METHOD | ENDPOINT                  | TOKEN  | ROLE         | DESCRIPTION                               | POST PARAMS                | RETURNS                        |
| ------ | ------------------------- | ------ | ------------ | ----------------------------------------- | -------------------------- | -------------------------------|
| GET    | /classDate/student/       | YES    | Student      | Gets all classDateByStudentEmail          | -                          | [{ Student }]                  |
| POST   | /classDate/               | YES    | Student      | Creates a classDate                       | -                          | Student created sucessfully    |
| PUT    | /classDate/:id            | YES    | Student      | Updates a specific booking                | student_id                 | Student updated successfully   |
| DELETE | /classDate/:id            | YES    | Student      | Deletes a specific booking                | student_id                 | Student deleted sucessfully    |

</details>


<details>
<summary>:point_right: Student Favourites</summary>

| METHOD | ENDPOINT                      | TOKEN  | ROLE           | DESCRIPTION                               | POST PARAMS                | RETURNS                        |
| ------ | -------------------------     | ------ | ------------   | ----------------------------------------- | -------------------------- | -------------------------------|
| GET    | /favouriteTeacher/            | YES    | student        | Gets all classrooms                       | -                          | [{ booking }]                  |
| POST   | /favouriteTeacher/            | YES    | student        | Creates a classroom                       | -                          | Classroom created sucessfully  |
| DELETE | /favouriteTeacher/:teacher_id | YES    | student        | Deletes a specific classroom              | classroom_id               | Classroom deleted sucessfully  |

</details>

<details>
<summary>:point_right: Student ratings</summary>

| METHOD | ENDPOINT                  | TOKEN  | ROLE         | DESCRIPTION                               | POST PARAMS                | RETURNS                           |
| ------ | ------------------------- | ------ | ------------ | ----------------------------------------- | -------------------------- | --------------------------------- |
| GET    | ratings/student/          | YES    | student       | Gets all subscriptions                    | -                          | [{ subscriptions }]               |

</details>

<details>
<summary>:point_right: Teacher Info</summary>

| METHOD | ENDPOINT                  | TOKEN  | ROLE         | DESCRIPTION                               | POST PARAMS                | RETURNS                           |
| ------ | ------------------------- | ------ | ------------ | ----------------------------------------- | -------------------------- | --------------------------------- |
| PUT    | /teacher/                 | YES    | teacher       | Gets all teachers                         | -                          | [{ teachers }]                    |

</details>

<details>
<summary>:point_right: Teacher classDates</summary>

| METHOD | ENDPOINT                  | TOKEN  | ROLE         | DESCRIPTION                               | POST PARAMS                | RETURNS                           |
| ------ | ------------------------- | ------ | ------------ | ----------------------------------------- | -------------------------- | --------------------------------- |
| GET    | /teacherClassDate/        | YES    | Teacher      | Updates a specific teacher                | -                          | Teacher updated successfully      |


</details>

<details>
<summary>:point_right: Teacher timetable</summary>

| METHOD | ENDPOINT                  | TOKEN  | ROLE         | DESCRIPTION                               | POST PARAMS                | RETURNS                           |
| ------ | ------------------------- | ------ | ------------ | ----------------------------------------- | -------------------------- | --------------------------------- |
| GET    | /timeTable/               | YES    | teacher      | Gets all teachers                         | -                          | [{ teachers }]                    |
| POST   | /timeTable/               | YES    | teacher      | Creates a teacher                         | -                          | Teacher created sucessfully       |
| PUT    | timeTable/:id             | YES    | teacher      | Updates a specific teacher                | teacher_id                 | Teacher updated successfully      |
| DELETE | timeTable/:id             | YES    | teacher      | Deletes a specific teacher                | teacher_id                 | Teacher deleted sucessfully       |

</details>

<details>
<summary>:point_right: Teacher ratings</summary>

| METHOD | ENDPOINT                  | TOKEN  | ROLE         | DESCRIPTION                               | POST PARAMS                | RETURNS                           |
| ------ | ------------------------- | ------ | ------------ | ----------------------------------------- | -------------------------- | --------------------------------- |
| GET    | /ratings/teacher/         | YES    | teacher      | Gets all teachers                         | -                          | [{ teachers }]                    |

</details>

<details>
<summary>:point_right: Teacher subjects</summary>

| METHOD | ENDPOINT                  | TOKEN  | ROLE         | DESCRIPTION                               | POST PARAMS                | RETURNS                           |
| ------ | ------------------------- | ------ | ------------ | ----------------------------------------- | -------------------------- | --------------------------------- |
| GET    | /subject/                 | YES    | teacher      | Gets all teachers                         | -                          | [{ teachers }]                    |
| POST   | /subject/                 | YES    | teacher      | Creates a teacher                         | -                          | Teacher created sucessfully       |
| DELETE | /subject/                 | YES    | teacher      | Deletes a specific teacher                | -                          | Teacher deleted sucessfully       |

</details>
