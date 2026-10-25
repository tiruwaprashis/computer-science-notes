# 5. Database Management System and Information Systems

## 5.1 Basic knowledge of Database Management System

### Data, Information, Knowledge and Wisdom

- **Data:** It means raw, unprocessed, isolated facts & figures that carry no meaning on their own. It may be numbers, text, symbols, dates, images, audio or video. Ex:- 25, "Ram", 9841000000 are just data.
- **Information**
  → Data that has been processed & organized so that it becomes meaningful & useful for decision making. Ex:- "Ram, aged 25, has balance Rs 50,000"
- **Knowledge**
  → It is an information combined with experience / rules that helps to take action.
- **Wisdom**
  → It is the applied judgement built on knowledge.

The chain is: **Data → Information → Knowledge → Wisdom**

---

### ◆ DBMS

→ It is a software system that enables users to define, create, maintain & control access to a database, acting as an interface between the database and its end users / application programs so that data remains organized, consistent and easily accessible. Ex:- Oracle, MySQL, MS SQL Server, PostgreSQL, MongoDB, MS Access.

→ A database is an organized, structured collection of logically related data stored electronically. Ex:- A Bank's database holding all customers, accounts & transactions.

**Architecture Flow**

```text
        +----------------------------------------------+
        |              USERS / APPLICATIONS            |
        |       End users · Programmers · DBA          |
        +----------------------------------------------+
             queries |                     ^ results
                     v                     |
        +----------------------------------------------+
        |                DBMS SOFTWARE                 |
        |  +-------------+ +-----------+ +-------------+|
        |  | DDL/DML     | | Query     | | Transaction ||
        |  | Processor   | | Optimizer | | & Recovery  ||
        |  |             | |           | | Manager     ||
        |  +-------------+ +-----------+ +-------------+|
        +----------------------------------------------+
                     |                     ^
                     v                     |
                  +----------------+
                  |    DATABASE    |
                  | Tables·Indexes |
                  |   · Metadata   |
                  +----------------+
```

### Objectives / Roles

→ To store large volumes of data in an organized & central manner.
→ To reduce data redundancy / repetition & maintain data consistency.
→ To provide secured, controlled and concurrent access to many users.
→ Provide data independence between applications and stored data.
→ To ensure integrity, backup and recovery.

### Main Functions

- **Data Definition**
  → defining the structure (tables, columns, constraints) using DDL.
- **Data Manipulation**
  → insert, update, delete and retrieve data using DML.
- **Data Security & Authorization**
  → granting/revoking access using Data Control Language (DCL).
- **Concurrency Control**
  → allows many users to work simultaneously without conflict.
- **Transaction Management**
  → ensuring ACID properties
- **Backup & Recovery**
  → restores database after failure

### Applications

| | |
| :--- | :--- |
| Banking | Telecom |
| Airline / railway reservation | Hospitals |
| Universities | Government records |
| E-commerce | Payroll systems |

**Conclusion**
→ Thus, a DBMS provides an efficient, safe & shared environment for handling data, so that every modern bank such as RBB depends on it.

### Advantages

- **Controlled redundancy**
  → data not repeated, saving storage
- **Data consistency**
  → one correct copy for everyone
- **Data sharing & concurrency**
  → many users at once
- **Data integrity**
  → constraints keep data valid
- **Security**
  → role-based access limits to authorized users.
- **Backup & recovery**
  → restores db after failure.
- **Data independence**
  → applications unaffected by storage-level changes

### Disadvantages

→ High cost of software, hardware and trained manpower / Database Administrator (DBA).
→ Complex design & maintenance
→ Centralized failure impact, a single crash can affect all users.
→ Unnecessary overhead for very small / simple applications.

### Components of a Database System

1. **Hardware:** physical devices, storage disks
2. **Software:** OS, applications, DBMS software
3. **Data:**
4. **Procedures:** Login, Backup, recovery
5. **People:** DBA, end users

---

### Q.1 Differentiate between DBMS & traditional file-processing system with a diagram.

```text
   File processing system                      DBMS

 [Program A] ---- [File 1]            [Program A] ----+
 [Program B] ---- [File 2]            [Program B] ----+---> [ DBMS ] ---> [Database]
 [Program C] ---- [File 3]            [Program C] ----+
```

| Basis | File processing system | DBMS |
| :--- | :--- | :--- |
| ① Diagram | Each program has its own file | All programs share one DBMS / database |
| ② Redundancy | High redundancy | Controlled |
| ③ Consistency | Low consistency | High |
| ④ Data sharing | Difficult data sharing | Easy |
| ⑤ Security | Security weak | Strong |
| ⑥ Integrity | Integrity is hard to enforce | Enforced by constraints |
| ⑦ Query language | Non-standard Query Language | Powerful SQL |
| ⑧ Data independence | No | Yes |
| ⑨ Backup / Recovery | Manual Backup/Recovery | Automatic |

**Disadvantages / Problems of File System**
- Data redundancy & inconsistency
- Difficult to access
- Data isolation → hard to combine scattered data
- Integrity problems
- Concurrency & security problems

---

### Q.2 Explain the ACID properties of a transaction with a banking example.

→ A transaction is a single logical unit of work. Eg:- a fund transfer = debit + credit. Every transaction must satisfy ACID:

- **Atomicity**
  → All operations happen fully, or none at all (all or nothing).
- **Consistency**
  → A transaction does not allow the database to enter an invalid state.
- **Isolation**
  → Concurrent transactions do not interfere with each other.
- **Durability**
  → Once committed, changes are permanent even after a crash.

**Banking Example**
→ When RBB transfers Rs. 10,000 from Account A to B;
- **Atomicity** ensures transactions (if the system crashes midway, the transaction is fully rolled back & the customer loses nothing.)
- **Consistency** ensure the account balance never goes negative, if a withdrawal exceeds the funds, instead it shows "insufficient balance".
- **Isolation** ensures if 2 people try to withdraw money from Account A at the same time, the database puts them in a line & process them one by one.
- **Durability** ensures that once "Transaction Successful" the update is saved permanently even if the bank still suffers power failure.

---

### ★ Types of DBMS / Data Models

→ It is a set of concepts to describe the structure of a database.

#### 1. Hierarchical Database Model
→ tree like structure with one to many relationships.
→ It was used in IBM's Information Management System (IMS).

```text
                         [ Bank ]
             +----------------+----------------+
       [Finance Dept]     [HR Dept]        [IT dept]
         +------+-----+    +-----+-----+    +-----+-----+
     [Staff] [Manager]  [Staff] [Manager] [Staff] [Manager]
```

#### 2. Network Model
→ graph like structure with many to many relationships.
→ a child can have many parents.
→ used by Integrated Database Management System (IDMS).

```text
                        [ Bank ]
              +-------------+-------------+
         [Customer]     [Manager]       [Staff]
              \   \       /  \  \       /   /
               \   +-----+----+--+-----+   /
                +-----> [Accounts]  <------+
                +-----> [Balance]   <------+
         (each of Customer, Manager and Staff links to both Accounts and Balance)
```

#### 3. Relational Model (RDBMS)
→ data in 2-dimensional table of rows and columns
→ Oracle, MySQL, SQL Server

```text
 +----------------+ 1        * +--------------------+
 | Branch         |------------| Employees          |
 | PK branch_id   |            | PK employee_id     |
 | branch_name    |            | FK branch_id       |
 | address        |            | employee_name      |
 +----------------+            | address            |
        | 1                    +--------------------+
        | *                              | 1
 +----------------+                      | *
 | Customer       | 1        * +--------------------+
 | PK customer_id |------------| Transactions       |
 | customer_name  |            | PK transaction_id  |
 | address        |            | account_no (FK)    |
 +----------------+            | type               |
        | 1                    +--------------------+
        | *
 +----------------+
 | Account        |   (m:n)
 | PK account_no  |
 | FK branch_id   |
 | type           |
 +----------------+
```

#### 4. Object-Oriented / Object-Relational Model
→ stores data as objects
→ useful for complex data.

```text
                      class: Account
             +------------------+------------------+
      SavingsAccount      CurrentAccount       LoanAccount
   (objects)                                
   calculateInterest()  calculateInterest()  calculateInterest()
   Withdraw()           Withdraw()           Withdraw()
```

#### 5. NoSQL DBMS
→ Document / key-value / column
→ MongoDB, Cassandra

---

### ① Three-level architecture

```text
External    +-------------+  +----------------------+  +----------------+
Level       | View 1:     |  | View 2: loan officer |  | View 3: auditor|
            | teller      |  |                      |  |                |
            +------+------+  +-----------+----------+  +--------+-------+
                   \                     |                      /     } logical data
                    \                    |                     /      } independence
Conceptual  +---------------------------------------------------+
Level       | CONCEPTUAL SCHEMA: entities, attributes,          |
            | relationships, constraints                        |
            +--------------------------+------------------------+     } physical data
                                       ^                                } independence
                                       v
Internal    +---------------------------------------------------+
Level       | INTERNAL SCHEMA: files, record layout, indexes,   |
            | access paths                                      |
            +--------------------------+------------------------+
                                       ^
                                       v
                          +--------------------------+
                          |  stored database (disk)  |
                          +--------------------------+
```
*Fig: 3-level (ANSI/SPARC) architecture*

---

### ② Explain SQL command types with examples and explain joins.

| Group | Purpose | Commands |
| :--- | :--- | :--- |
| DDL | Define structure | CREATE, ALTER, DROP, RENAME |
| DML | Work with data | INSERT, UPDATE, DELETE (SELECT sometimes listed as DQL) |
| DCL | Permissions | GRANT, REVOKE |
| TCL | Transactions | COMMIT, ROLLBACK, SAVEPOINT |

- `CREATE TABLE Customer (CustID INT PRIMARY KEY, NAME VARCHAR(50));` (DDL)
- `INSERT INTO Customer VALUES (101, 'Sita');`
  `UPDATE Account SET Balance = Balance - 500 WHERE AccNo = 1001;` (DML)
- `SELECT * FROM Customer WHERE CustID = 101;`
  `GRANT SELECT ON Customer TO teller;` (DCL)
- DELETE removes chosen rows (can roll back); TRUNCATE removes all rows, keep table; DROP removes the table itself.

| Join | Returns |
| :--- | :--- |
| INNER | Only matching rows from both table |
| LEFT (OUTER) | All left rows + matches; NULL where no match |
| RIGHT (OUTER) | All right rows + matches; NULL where no match |
| FULL OUTER | All rows from both; NULL where no match |

**Syntax:**
```sql
SELECT c.Name, a.Balance FROM Customer c
INNER JOIN Account a ON c.CustID = a.CustID;
```

---

## 5.2 Table, Record, Relationship and Indexing

### LQ.1 Explain keys, relationships and integrity constraints with an ER diagram. Differentiate PK and FK.

| CustID | Name | CitizenshipNo | City |
| :--- | :--- | :--- | :--- |
| C01 | Ram Thapa | 27-01-111 | Kathmandu |
| C02 | Sita Rai | 31-02-222 | Pokhara |
| C03 | Ram Thapa | 45-03-333 | Butwal |

```text
+------------------------------------------------------------+
| SUPER KEYS: {CustID}  {CustID, Name}  {CitizenshipNo, City}|
|   +----------------------------------------------------+   |
|   | CANDIDATE KEYS                                     |   |
|   |   +------------------+   +---------------------+   |   |
|   |   | PRIMARY KEY      |   | ALTERNATE KEY       |   |   |
|   |   | CustID           |   | CitizenshipNo       |   |   |
|   |   +------------------+   +---------------------+   |   |
|   +----------------------------------------------------+   |
+------------------------------------------------------------+
```

- CustID : unique for every row → good key
- CitizenshipNo : also unique → another good key
- Name : "Ram Thapa" same → NOT unique, cannot be a key

| Key | Meaning | Bank example |
| :--- | :--- | :--- |
| Super key | Any column set that is unique per row (extras allowed) | {CustID, Name} |
| Candidate key | Super key with NOTHING extra (remove a column → not unique) | {CustID}, {CitizenshipNo} |
| Primary key (PK) | The ONE candidate key we choose. Unique, never NULL, one per table | CustID |
| Alternate key | Candidate keys we did not choose | CitizenshipNo |
| Composite key | Key made of 2+ columns together (each alone is not unique) | (CustID, AccNo) in HOLDER table |
| Foreign key (FK) | Column that holds the PK of ANOTHER table - it links the tables | ACCOUNT.CustID → CUSTOMER.CustID |

- **Composite key example** - [joint account (HOLDER table)]

| CustID | AccNo |
| :--- | :--- |
| C101 | A1 |
| C101 | A2 |

here C101 repeats and A1/A2 can repeat when alone but the PAIR (CustID, AccNo) is unique.

- **Bank's**

| Purpose | Primary Key | Foreign Key |
| :--- | :--- | :--- |
| Purpose | Identifies row in its OWN table | Links to PK of ANOTHER table |
| NULL | Not allowed | Allowed |
| Duplicates | Not allowed | Allowed |
| How many per table | Only ONE | Can be MANY |
| Enforces | Entity integrity | Referential Integrity |

- **Relationships**
  - 1:1 (employee - passport)
  - 1:N (one customer, many accounts)
  - M:N (students - courses)

- **ER symbols**
  - rectangle (entity)
  - oval (attribute)
  - diamond (relationship)
  - underline (key attribute)
  - double rectangle (weak entity), multi-valued
  - dashed ellipse (derived)

- **Integrity**
  - entity integrity (PK not null / unique)
  - referential integrity (FK must match an existing PK or be Null - no account for a non-existent customer)
  - domain (valid type/range)

```text
 (CustID) (Name)      (AccNo)   (Balance)                     (BranchCode)
      \     /             \      /                                 |
     [ CUSTOMER ]  M--<holds>--N  [ ACCOUNT ]  N--<kept at>--1  [ BRANCH ]--(BranchName)
      /       \                       |
 (Phone)     (Age)                  (Type)
 multi-valued derived
```
*Fig: ER Diagram of customers, accounts and branches*

---

### LQ.2 What is normalisation? Explain 1NF, 2NF, 3NF with an example.

**Def**
→ Splitting a table into smaller related tables to reduce redundancy and avoid insert / update / delete anomalies.

→ Each step splits a table into smaller tables without losing information.

```text
[Unnormalized table] → [1NF] → [2NF] → [3NF] → [BCNF]
                         |        |        |        |
                  remove repeating  remove   remove   every determinant =
                  groups; atomic    partial  transitive  a candidate key
                  values            dependencies dependencies
```
*Fig: Steps of normalization*

#### ① 1NF (First Normal Form)
→ Data must be stored in a table with rows and column and each column should contain individual values.

**Project table**

| CustID | AccNo | CustName | Balance |
| :--- | :--- | :--- | :--- |
| C01 | A100, A101 | Sita | 50000, 2500 |
| C02 | A102 | Ram | 1000 |
| C03 | A103, A104 | Hari | 75000, 70000 |

**After 1NF**

| CustID | AccNo | CustName | Balance |
| :--- | :--- | :--- | :--- |
| C01 | A100 | Sita | 50,000 |
| C01 | A101 | Sita | 2500 |
| C02 | A102 | Ram | 1000 |
| C03 | A103 | Hari | 75000 |
| C03 | A104 | Hari | 70,000 |

#### ② 2NF
→ Must be in 1NF
→ All non-key attributes should be fully dependent on the primary key (no partial dependencies).

**Table 1 (Customer)** (PK: CustID)

| CustID | CustName |
| :--- | :--- |
| C01 | Sita |
| C02 | Ram |
| C03 | Hari |

**Table 2 (Account)** (FK: CustID)

| CustID | AccNo | Balance |
| :--- | :--- | :--- |
| C01 | A100 | 50,000 |
| C01 | A101 | 2,500 |
| C02 | A102 | 1000 |
| C03 | A103 | 75,000 |
| C03 | A104 | 70,000 |

#### ③ 3NF
→ Must be in 2NF
→ Non-key attributes should not depend on other non-key attributes

**Table 1: Customer** (Same as 2NF)

| CustID | CustName |
| :--- | :--- |
| C01 | Sita |
| C02 | Ram |
| C03 | Hari |

**Table 2: Accounts**

| AccNo | Balance |
| :--- | :--- |
| A100 | 50,000 |
| A101 | 2,500 |
| A102 | 1000 |
| A103 | 75,000 |
| A104 | 70,000 |

**Table 3: Customer Account**

| CustID | AccNo |
| :--- | :--- |
| C01 | A100 |
| C01 | A101 |
| C02 | A102 |
| C03 | A103 |
| C03 | A104 |

#### ④ Boyce-Codd Normal Form (BCNF)
→ Must be in 3NF
→ If a table contain more than one composite key attributes and should be possible the one attribute of both composite key are matched.

**Suppose, for 2NF**

| CustID | AccNo | CustName | Balance | BranchCode | BranchName |
| :--- | :--- | :--- | :--- | :--- | :--- |
| C01 | A101 | Sita Rai | 50,000 | B01 | Ktm |
| C01 | A102 | Sita Rai | 20,000 | B02 | Npj |
| C03 | A101 | Ram Thapa | 50,000 | B01 | Ktm |
| C02 | A103 | Hari Thapa | 75000 | B01 | Ktm |

Check for the key (CustID, AccNo)
Here, CustName depends only on CustID } partial dependency
Balance depends only on AccNo } problem

so split them,

**CUSTOMER Table** (Key: CustID)

| CustID | CustName |
| :--- | :--- |
| C01 | Sita Rai |
| C02 | Hari Thapa |
| C03 | Ram Thapa |

**ACCOUNT Table** (key: AccNo)

| AccNo | Balance | BranchCode | BranchName |
| :--- | :--- | :--- | :--- |
| A101 | 50,000 | B01 | Ktm |
| A102 | 20,000 | B02 | Npj |
| A103 | 75,000 | B01 | Ktm |

**HOLDER** (key: CustID + AccNo)

| CustID | AccNo |
| :--- | :--- |
| C01 | A101 |
| C01 | A102 |
| C03 | A101 |
| C02 | A103 |

Name are now stored once per customer and balance once per account. This is 2NF.

**Now, for 3NF**
In table Account non-key column "BranchName" depends only on another non-key column "BranchCode". (transitive dependency)

Again split them,

| BranchCode | BranchName |
| :--- | :--- |
| B01 | Ktm |
| B02 | Npj |

Now, Account table would be,

| AccNo | Balance | BranchCode |
| :--- | :--- | :--- |
| A101 | 50,000 | B01 |
| A102 | 20,000 | B02 |
| A103 | 75,000 | B01 |

This is in 3NF.

**Now rule for BCNF**
→ for every dependency X → Y, X must be a key.

| Table | Dependency | Is the left side a key? |
| :--- | :--- | :--- |
| CUSTOMER | CustID → CustName | Yes |
| BRANCH | BranchCode → BranchName | Yes |
| ACCOUNT | AccNo → Balance, BranchCode | Yes |
| HOLDER | CustID → AccNo | Yes |

so this design is already in BCNF.

---

### LQ.3 What is indexing? Types, advantage and disadvantages.

**Def**
→ It is an extra data structure (sorted keys + pointers to rows) that lets the DBMS find rows without a full table scan - like a book index.

**Structures**
→ B/B+ tree (exact + range, most common, search cost O(log n))
  hash (exact match only)
  bitmap (few distinct values)

```text
                      [ 30 | 60 ]                    ← root
                 /         |          \
          [10|20]       [40|50]        [70|80]       ← internal nodes
          /  |  \       /  |  \        /  |  \
       [5 8][10 15][20 25][30 35][40 45][50 55][60 65][70 75][80 90]   ← leaf nodes (linked →)
```
leaf nodes hold all keys with pointers to the rows and are linked for range scans

*Fig: A B+ tree index.*

| Type | Meaning |
| :--- | :--- |
| Primary index | On the ordering key/PK |
| Clustered | Reorders the actual rows; only ONE per table. |
| Non-clustered (secondary) | Separate structure with pointers; MANY allowed. |
| Dense | Entry for every record |
| Sparse | Entry for some records (eg: one per block); data file must be ordered |
| Unique / Composite | No duplicates / no more than one column |

- **Advantages:** faster SELECT, JOIN, ORDER BY, GROUP BY; enforces uniqueness.
- **Disadvantages:** extra storage; slower INSERT/UPDATE/DELETE; maintenance

**Conclusion**
→ Indexing speeds up "reads at the cost of storage and slower writes" - index only frequently searched columns such as account number.

---

## 5.3 Data Warehousing and Process in Data Warehousing

### Q.1 Define data warehouse. Differentiate from operational database.

**Def** A subject-oriented, integrated, time-variant, non-volatile collection of data in support of management decisions.

| SITN | Meaning |
| :--- | :--- |
| Subject-oriented | Organized around customer, loan, deposit - not applications |
| Integrated | Many sources made consistent (one coding scheme, one customer identity) |
| Time-variant | Keeps years of history for trend analysis |
| Non-volatile | Loaded and read; not updated or deleted in day-to-day work |

```text
Data sources        Staging           Storage                     Analysis

[Core banking     ]           [Data mart: credit] [Data mart: deposits]     [OLAP analysis]
[(OLTP)           ]                     ^                ^                  
[Cards & ATM      ]   →  [ETL /    ] →  [   DATA WAREHOUSE        ] →       [Reports &     ]
[switch           ]      [staging  ]    [ integrated, historical  ]         [dashboards    ]
[Loan system      ]      [area     ]    [ data                    ] →       [Data Mining   ]
[External data    ]                              |
[(files, feeds)   ]                     [Metadata repository]
```
*Fig: Architecture of a data warehouse for a bank*

**ETL**
- **Extract** → read from sources; full first load, incremental later
- **Transform** → clean, remove duplicates, standardise, integrate, derive/aggregate
- **Load** → write into fact/dimension tables
- **Variant:** ELT loads raw data first and transforms inside the warehouse.

| Basis | Online Transaction Process (OLTP) (Operational) | Online Analytical Process (OLAP) / Data warehouse |
| :--- | :--- | :--- |
| Purpose | Run daily operations | Analysis and decisions |
| Data | Current, detailed | Historical, summarised |
| Operations | Short insert/update/delete | Complex read-only queries |
| Design | Normalised (ER, 3NF) | Denormalised (star / snowflake) |
| Users | Tellers, customers (many) | Managers, analysts (few) |
| Measure | Transactions per second | Query response time |

- **Advantages:** one consistent view, history, better decisions, no load on live systems
- **Limitations:** high cost, long development, data only as fresh as last load, security risk (everything in one place).
- **Banking use:** regulatory/management reports, credit scoring, fraud detection, branch comparison

---

### Q.2 What is data mining? Explain techniques and process; differentiate from data warehousing.

**Def**
→ Discovering useful patterns, relationships and trends in large data using statistics, machine learning and database methods.

| Technique | Purpose | Bank example |
| :--- | :--- | :--- |
| Classification | Assign to know class | Good/bad credit risk |
| Regression | Predict a number | Expected loan loss |
| Clustering | Group similar items, no classes given | Customer segmentation |
| Association rules | Items occuring together | Salary account holders take credit cards |
| Anomaly detection | Find unusual cases | Fraud, money-laundering alerts |

```text
[Data] → [selection] → [Pre-processing] → [Transformation] → [Data mining] → [Evaluation]
              |               |                  |                 |               |
         target data     cleaned data     transformed data      patterns       [knowledge]
```
*Fig: Knowledge discovery in databases (KDD)*

**Conclusion**
→ The warehouse stores the data; data mining finds the hidden value in it.

```text
 [DIM_DATE]                                        [DIM_BRANCH]
 DateKey (PK)  1 ----+                   +---- 1   BranchKey (PK)
 Day, Month, Year    N                   N        Branch, Province
                  [ FACT_TRANSACTION ]
 [DIM_CUSTOMER]   DateKey (FK)                     [DIM_PRODUCT]
 CustomerKey (PK) 1-N CustomerKey (FK)   N --- 1   ProductKey (PK)
 Name, Segment      BranchKey (FK)                 Type, Scheme
                    ProductKey (FK)
                    Amount, Count
```
*Fig: Star schema for banking transactions*

---

## 5.4 Basics of HTML, Script, Stylesheet, XML, Web Server and Proxy Server

### Q.1 Explain HTML, CSS, JavaScript and XML. Differentiate HTML from XML.

- **HTML** → It is not a programming language.

  Syntax:
  ```html
  <html>
    <head>
      <title> </title>
    </head>
    <body>
    </body>
  </html>
  ```

- **CSS** (Cascading Style Sheets)
  → controls presentation (colour, font, layout)

  Three ways:
  1. Inline (style attribute)
  2. Internal (`<style>` in head)
  3. External (.css file via `<link>` - best for a whole site)

- **JavaScript:** client-side scripting language giving behaviour (form checks, events, DOM changes). Runs in browser (fast).
  Server-side (PHP, Java, Python, ASP.NET) runs on the server, reads the database, hides code.

- **XML** (Extensible Markup Language)
  → for storing and transporting data with user-defined tags. Example:
  ```xml
  <customer>
    <id>101</id>
    <name>Sita</name>
  </customer>
  ```

| Basis | HTML | XML |
| :--- | :--- | :--- |
| Purpose | Display data | Describe and carry data |
| Tags | Predefined (`<h1>`, `<p>`, `<a href>`, `<table>`, `<form>`) | User-defined |
| Case | Not case-sensitive (tags) | Case-sensitive |
| Closing tags | Some optional | Mandatory |
| Errors | Browser forgives | Processing stops |

∴ HTML = structure, CSS = style, JavaScript = behaviour, XML = data
Banking tie-in: ISO 20022 payment messages use XML

---

### Q.2 Explain web server and proxy server with working, types and uses.

**1. Web server:** software/computer that stores web content and answers HTTP/HTTPS requests. Ex:- Apache, Nginx, IIS.

- **Working (7 steps)**
  URL typed → DNS gives IP → browser connects (HTTP 80, HTTPS 443 with TLS) → sends HTTP request (GET/POST) → server finds file or runs script + DB query → sends response with status code → browser displays page.

- **Status codes:** 200 OK, 301 redirect, 404 Not Found, 500 Server Error. HTTP is stateless - sessions use cookies

**2. Proxy server:** intermediary that sends request on behalf of clients and returns replies.

**Types**

```text
(a) Forward proxy                          (b) Reverse proxy

 staff PC ┐                                  [customers   ]            ┌→ [Web server 1]
 staff PC ┼→ [Forward proxy] → [Internet]   [(Internet)   ] → [Reverse proxy] ┼→ [WS 2]
 staff PC ┘                                                           └→ [WS 3]

 acts for clients; filtering, caching,      acts for the servers: load balancing,
 hides the clients.                         TLS, caching, hides the servers
```

- **Challenges**
  → single point of failure
  → HTTPS injection and privacy concerns
  → setup/maintenance

- **Bank example**
  → staff browse through a forward proxy with filtering; internet banking servers sit behind a reverse proxy and web-application firewall.

---

## 5.5 Disaster Recovery Planning (DRP)

### Q.1 What is DRP? Explain its steps, RTO and RPO, recovery sites, backups and testing. Differentiate DR from BCP.

**Def** A documented, tested, regularly updated plan describing who does what, when and how to recover IT systems, data and infrastructure after a disaster (fire, flood, earthquake, long power failure, cyber attack).

**Why a bank needs it**
→ payments, ATM & internet banking depend on IT.
→ downtime means financial loss, lost trust and regulatory breach (NRB expects BCP/DR arrangements, backup and DR sites, periodic testing).

**Objectives**
→ protect critical data
→ minimise downtime and data loss
→ orderly recovery in priority order
→ limit financial / reputation damage

**DRP development lifecycle**
1. **Management support & policy**
   → budget, scope, DR committee
2. **Risk assessment**
   → assets, threats, vulnerabilities
3. **Business Impact Analysis (BIA)**
   → dependencies, impact over time; set MTD (Maximum Tolerable Downtime)
4. **Select recovery strategies**
   → backup & restore
   → alternate site
   → replication/clustering
   → spare hardware
   → cheapest option that still meets RTO/RPO
5. **Write the plan**
   → runbooks, contact lists, inventories; keep printed and off-site copies.
6. **Awareness & Training**
   → cross-train; no dependence on one person
7. **Testing** and 8. **Maintenance**
   → review at least yearly and after every change or incident.

- **RTO** = maximum acceptable downtime (how fast must we be back).
  **RPO** = maximum acceptable data loss measured in time (decides backup/replication frequency).

MTD = longest tolerable outage; RTO + WRT (Work Recovery Time) ≤ MTD

{ RPO → Recovery Point Objective
{ RTO → Recovery Time Objective

**Working example of RPO & RTO on a timeline**

```text
 Last good                DISASTER           Service
 backup or replica        (15:00)            restored
 (22:00)                                     (19:00)
    |----------------------|///////////////////|
    |<---- data lost: 17 hours ---->|<-- downtime: 4 hours -->|  → time
      (the limit allowed is RPO)       (the limit allowed is RTO)
```

**Types of backup**

| Type | What it copies | Backup speed/size | Restore needs |
| :--- | :--- | :--- | :--- |
| Full | Everything, every time | Slowest, largest | 1 set - fastest restore |
| Incremental | Changes since the last backup of any type | Fastest, smallest | Last full + every incremental - slowest restore |
| Differential | Changes since the last full backup | Medium; grows daily | Last full + latest differential only (2 sets) |

**Recovery sites**

| Site | Description | Recovery time | Cost |
| :--- | :--- | :--- | :--- |
| Hot | Fully equipped, continuously update duplicate | Minutes-hours | Highest |
| Warm | Hardware and connectivity ready; data restored from backup | Hours-day | Medium |
| Cold | Empty shell; space, power, cooling only | Days-weeks | Lowest |
| Mirror / cloud DR | Active duplicate in real time / virtual infrastructure on demand | Near zero / minutes-hours | Very high / pay per use |

**Testing**
checklist (desk check) → Walkthrough/Tabletop → Simulation → Parallel → Full interruption (cutover).

Steps:
set objectives → run & record times → compare actual RTO/RPO → report gaps → update plan.
Frequency: restore tests monthly/quarterly; tabletop at least annually.

| Basis | DRP | Business continuity (BCP) |
| :--- | :--- | :--- |
| Scope | IT systems and data | Whole business: people, process, premises, IT |
| Aim | Restore technology | Keep critical services running |
| Timing | Mainly after the event | Before, during and after |
| Relationship | Subset of BCP | Umbrella plan |
| Owner | IT department | Senior management / board |

**Conclusion**
→ A tested DR plan with suitable RTO, RPO and recovery site lets a bank resume core banking quickly; DR is part of BCP and a DR site is a regulatory necessity.

### MCQ
- **Standards**
  - ISO 22301 = business continuity management
  - ISO/IEC 27031 = ICT readiness for BC
  - NIST SP 800-34 = IT contingency planning
- **3-2-1 rule**
  (3 copies, 2 media, 1 off-site)
