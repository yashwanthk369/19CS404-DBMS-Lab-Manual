# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:

<img width="1119" height="756" alt="Screenshot 2026-02-11 084319" src="https://github.com/user-attachments/assets/55d6f2c6-181a-436d-85e6-2c743ebe4e84" />

### Entities and Attributes

| Entity  |           Attributes (PK, FK)          |              Notes                 |
|---------|----------------------------------------|------------------------------------|
| Member  | MemberID(PK),Name,MemberType,StartDate | Each member has unique ID          |
| Program | ProgramID,ProgramName,Schedule         | Each members has multiple programs |
| Trainer | TrainerName,Specialization             | Trainer is assigned to a program   |
| Session | Duration,Date&Time,Status              | Program has seperate session       |
| Attend  | Date,Status                            | Each session has attendance        |
| Payment | PaymentID,Status                       | Member has to pay their fees       |

### Relationships and Constraints

| Relationship                  | Cardinality                   | Participation            | Notes                                                 |
| ----------------------------- | ----------------------------- | ------------------------ | ----------------------------------------------------- |
| Member – Payment              | 1:N                           | Total on Payment side    | One member can make multiple payments                 |
| Member – Session              | 1:N                           | Total on Session side    | One member can book multiple sessions                 |
| Trainer – Session             | 1:N                           | Total on Session side    | One trainer can handle many sessions                  |
| Member – Attendance – Session | M:N (resolved via Attendance) | Total on Attendance side | Attendance connects members and sessions              |
| Trainer – Program             | M:N                           | Partial on both sides    | Trainers can conduct multiple programs and vice versa |
| Member – Program              | M:N                           | Partial on both sides    | Members can join multiple programs                    |


### Assumptions

A member can join the same program only once at a time.

Each personal training session is handled by only one trainer.

Attendance is mandatory for every booked personal training session.

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:

<img width="1072" height="821" alt="WSQ1 drawio" src="https://github.com/user-attachments/assets/dcc067b6-f0c2-4e70-bb5f-deffb1764e60" />

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|              |            |               |       |
|              |            |               |       |
|              |            |               |       |

### Assumptions
- 
- 
- 

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:

<img width="1222" height="849" alt="Screenshot 2026-02-13 105139" src="https://github.com/user-attachments/assets/be7bbdd4-489a-4e12-a20d-af8c4ba4ae21" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|              |            |               |       |
|              |            |               |       |
|              |            |               |       |

### Assumptions
- 
- 
- 

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
