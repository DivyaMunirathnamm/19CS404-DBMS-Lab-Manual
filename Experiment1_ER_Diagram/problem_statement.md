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
<img width="1363" height="665" alt="CITY" src="https://github.com/user-attachments/assets/021b29af-61cc-4a5f-a23f-2b2a3e60d9aa" />


### Entities and Attributes
| Entity        | Attributes (PK, FK)                                                 | Notes                          |
|---------------|---------------------------------------------------------------------|--------------------------------|
| MEMBER        | Member_ID (PK), First_Name, Last_Name, DOB, Gender, Phone_No,Address| A registered person in the club |
| STAFF         | Staff_ID (PK), Name, Job_Desc, Job_Description                      | Employees who assist/manage     |
| TRAINER       | Trainer_ID (PK), Name, Age                                          | Specialized trainers for classes|
| FITNESS_CLUB  | Club_ID (PK), Name, Special                                         | Represents a fitness club branch|
| FITNESS_CLASS | Class_ID (PK), Duration                                             | Scheduled fitness session       |
| EQUIPMENT     | Equip_ID (PK), Equip_Name, Purchase_Date                            | Machines/tools used in classes  |
| PAYMENT       | Payment_ID (PK), Plan_Name, Amount, Mode                            | Payment details of members      |


### Relationships and Constraints
| Relationship                        | Cardinality | Participation         | Notes                                                                 |
|-------------------------------------|-------------|-----------------------|-----------------------------------------------------------------------|
| MEMBER – STAFF (TAKES)              | M:N         | Partial               | Members interact with multiple staff; staff assist many members       |
| STAFF – FITNESS_CLASS               | 1:M         | Total on class side   | One staff manages multiple classes; each class has one staff          |
| MEMBER – FITNESS_CLASS              | M:N         | Partial               | Members can enroll in multiple classes; classes have many members     |
| TRAINER – FITNESS_CLASS (WORKS_FOR) | M:N         | Partial               | Trainers can handle multiple classes; each class can have many trainers|
| FITNESS_CLASS – EQUIPMENT (ENGAGE_IN)| M:N        | Partial               | A class can use multiple equipment; equipment reused in different classes|
| FITNESS_CLUB – FITNESS_CLASS        | 1:M         | Total on class side   | Each club organizes many classes; each class belongs to one club      |
| FITNESS_CLUB – EQUIPMENT (USES)     | 1:M         | Total on equipment side| Each club owns multiple equipment; equipment belongs to one club      |
| FITNESS_CLUB – PAYMENT              | 1:M         | Total on payment side | Each club generates multiple payments                                |
### Assumptions
1.Each Member must belong to at least one Fitness Club indirectly through classes and payments.

2.A Fitness Class cannot exist without being associated with a Fitness Club.

3.Payments are always tied to a Fitness Club, not directly to trainers or staff.

4.Equipment belongs to a single club only, not shared across clubs.

5.A Trainer can be associated with multiple clubs via classes, but each class belongs to only one club.

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
<img width="1287" height="794" alt="LIB" src="https://github.com/user-attachments/assets/17377d33-4394-4c8a-bf33-e5f3e3cf4630" />


### Entities and Attributes
| Entity   | Attributes (PK, FK)                                      | Notes                                             |
|----------|----------------------------------------------------------|---------------------------------------------------|
| MEMBER   | Member_ID (PK), First_Name, Last_Name, DOB, Gender, Address | Represents a person registered in the library     |
| STAFF    | Staff_ID (PK), Name                                      | Library staff who manage events                   |
| EVENT    | Event_ID (PK), Event_Name, Description                   | Library events like workshops, seminars           |
| BOOK     | Book_ID (PK), Title, Author, Age                         | Books available in the library                    |
| LENDING  | Lend_ID (PK), Issue_Date, Return_Date (optional)         | Records lending/borrowing transactions            |
| LIBRARY  | Library_ID (PK), Name, Location, Eoption                 | Represents the library branch                     |

### Relationships and Constraints


| Relationship                     | Cardinality | Participation        | Notes                                                                 |
|----------------------------------|-------------|----------------------|----------------------------------------------------------------------|
| MEMBER – EVENT (MANAGES via STAFF) | 1:M         | Total on Event side  | Staff manages multiple events; each event is managed by one staff     |
| MEMBER – BOOK (BORROWS)          | M:N         | Partial              | Members can borrow many books; each book can be borrowed multiple times|
| MEMBER – LENDING                 | 1:M         | Total on Lending side| Each lending record belongs to one member                             |
| BOOK – LENDING                   | 1:M         | Total on Lending side| Each lending record is for one book                                   |
| EVENT – MEMBER                   | M:N         | Partial              | Members can participate in multiple events; each event has many members|

### Assumptions
1.A Member can borrow multiple books, but a lending record is created per transaction.

2.A Book can be borrowed multiple times by different members.

3.Each Lending must have an Issue_Date, and may have a Return_Date.

4.A Library may host multiple Events.

5.Each Event is managed by one Staff member, but a staff can manage many events.

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
<img width="1275" height="692" alt="RES" src="https://github.com/user-attachments/assets/1980b53f-3031-4f03-8871-accdde4ed828" />


### Entities and Attributes


| Entity       | Attributes (PK, FK)                                                   | Notes                                                  |
|--------------|----------------------------------------------------------------------|--------------------------------------------------------|
| Customer     | Customer_ID (PK), First_Name, Last_Name, Email, Phone_Number, Address | One customer can make many reservations and orders      |
| Reservation  | Reservation_ID (PK), Customer_ID (FK)                                | Made by a customer                                     |
| Table        | Table_ID (PK), Table_Number, Capacity, Location                      | Can be assigned to reservations                        |
| Menu_Items   | Item_ID (PK), Veg, Non-Veg                                           | Items in the restaurant menu                           |
| Order        | Order_ID (PK), Customer_ID (FK), Reservation_ID (FK), Order_Date, Total_Amount | Linked to customer and reservation      |

### Relationships and Constraints

| Relationship                     | Cardinality | Participation        | Notes                                                                 |
|----------------------------------|-------------|----------------------|----------------------------------------------------------------------|
| MEMBER – EVENT (MANAGES via STAFF) | 1:M         | Total on Event side  | Staff manages multiple events; each event is managed by one staff     |
| MEMBER – BOOK (BORROWS)          | M:N         | Partial              | Members can borrow many books; each book can be borrowed multiple times|
| MEMBER – LENDING                 | 1:M         | Total on Lending side| Each lending record belongs to one member                             |
| BOOK – LENDING                   | 1:M         | Total on Lending side| Each lending record is for one book                                   |
| EVENT – MEMBER                   | M:N         | Partial              | Members can participate in multiple events; each event has many members|


### Assumptions

1.Each reservation is associated with at least one customer.

2.Menu items are either Veg or Non-Veg but not both.

3.Orders must be linked to an existing customer and can optionally be linked to a reservation.

4.One table can be reused in multiple reservations.

5.Events are optional and depend on specific customer-service interactions.
## Instructions for Students
1.Complete all three scenarios (A, B, C).

2.Identify entities, relationships, and attributes for each.

3.Draw ER diagrams using draw.io / diagrams.net or hand-drawn & scanned.

4.Fill in all tables and assumptions for each scenario.

5.Export the completed Markdown (with diagrams) as a single PDF

