# (CSC 370) Database Systems - Complete Notes - Spring 2023
[TOC]

# Class Intro

>  Alex Thomo (thomo@uvic.ca)
>
> Office Hours:
>
> - Tuesday 9:00am-10:00am (https://uvic.zoom.us/j/81584166127)
> - Friday 9:00am-10:00am (https://uvic.zoom.us/j/81584166127)

## Content

This course is an introduction to database systems. Topics include database design, query languages, query optimization, concurrency control, and recovery from failures.

- Database design
- Relational Algebra
- SQL
- Data Analytics
- Security
- Query evaluation
- Transaction Management
- Recovery from System Failures

## Textbooks

**Database Systems: The Complete Book** - by Hector Garcia-Molina, Jeffrey D. Ullman, and Jennifer D. Widom Prentice Hall, 2nd Edition, ISBN: 0131873253

## Assignments

## Course Evaluation

- Assignments (20%) - (4 x 5%) 
- Midterm (25%)
- Final exam (55%)

## Lecture Slides

[Lecture 0](assets/L0.pdf) - Entity-Relationship Model

[Lecture 1](assets/L1.pdf) - From E/R Diagrams to Relations

[Lecture 2](assets/L2.pdf) - SQL



# Entity-Relationship Model

## Database design 

- designing a database:
  - what **information** the database must hold
  - what **relationships** are there among components of that information.
- Notation for expressing designs: **<u>Entity-Relationship (E/R) model</u>**

![image-20230125200303563](assets/image-20230125200303563.png)

## Elements of the Entity-Relationship Model

| Name          | Shape/Color      | Example                                                      |
| ------------- | ---------------- | ------------------------------------------------------------ |
| Entity Sets   | Square / Green   | ![image-20230125200514521](assets/image-20230125200514521.png) |
| Attributes    | Circle / White   | ![image-20230125200525525](assets/image-20230125200525525.png) |
| Relationships | Diamond / Yellow | ![image-20230125200533732](assets/image-20230125200533732.png) |

#### Example

![image-20230125200608590](assets/image-20230125200608590.png)

## Visualizing Binary Entity-Relationship Relationships

- They are just sets of pairs:

| Movies         | Stars                 |
| -------------- | --------------------- |
| Basic Instinct | Sharon Stone          |
| Total recall   | Arnold Schwarzenegger |
| Total recall   | Sharon Stone          |

## Multiplicity of Relationships

#### Many-To-One

![image-20230125200930142](assets/image-20230125200930142.png)

#### One-To-One

![image-20230125200946115](assets/image-20230125200946115.png)

#### Many-To-Many

![image-20230125201009145](assets/image-20230125201009145.png)

**Note:** Sometimes binary relationships aren’t enough!

Ex. 

![image-20230125201210390](assets/image-20230125201210390.png)

>  Q: What could go wrong with this design? 
>
> A: Problem with finding which stars a studio is paying for a given movie.

## Why some studio-movie-star triples can be invalid?

Example:

**Carolco Pictures** paid **Arnold Schwarzenegger** for **Total Recall TriStar** paid **Sharon Ston**e for **Total Recall**.

- Using “Owns” and “Stars-In” we will have the following triples: (CP, TR, AS) <u>(CP, TR, SS)</u> <u>(TS, TR, AS)</u> (TS, TR, SS)

- The <u>second</u> and the <u>third</u> triples aren’t valid.
- If we consider the collection of all the valid triples, it is nothing else but a **three way relationship** between **Studios, Movies** and **Stars**

Solution: (Three way relationship)

![image-20230125201627843](assets/image-20230125201627843.png)

## Attributes on Relationships

![image-20230125201701272](assets/image-20230125201701272.png)

## Roles in a Relationship

- An entity set can appear two or more times in a relationship. 
- Each line to the entity set represents a different role.

![image-20230125205428623](assets/image-20230125205428623.png)

- A movie may have **many sequels**, but for each sequel there is **only one original movie.**

![image-20230125205523197](assets/image-20230125205523197.png)

![image-20230125205543140](assets/image-20230125205543140.png)

## "Bars-Beer-Drinkers" Example

- Bars sell some beers.
- Drinkers like some beers.
- Drinkers frequent some bars.
- What would the E/R diagram be?

![image-20230125205708066](assets/image-20230125205708066.png)

#### "Bar-Beers-Drinkers" Multiway Relationship

Suppose that drinkers will only drink certain beers at certain bars.

![image-20230125205812647](assets/image-20230125205812647.png)

## A Typical Relationship Set

| Bar       | Drinker | Beer       |
| --------- | ------- | ---------- |
| Joe's Bar | Ann     | Miller     |
| Sue's Bar | Ann     | Bud        |
| Sue's Bar | Ann     | Pete's ale |
| Joe's Bar | Bob     | Bud        |
| Joe's Bar | Bob     | Miller     |
| Joe's Bar | Cal     | Miller     |
| Sue's Bar | Cal     | Bud Lite   |

## Multiple Relationships Between Two Entity Sets

![image-20230125210424062](assets/image-20230125210424062.png)

## “Exactly one” Multiplicity

![image-20230125210449176](assets/image-20230125210449176.png)

- Some beers are not the best-seller of any manufacturer, so a rounded arrow to Manfs would be inappropriate.
- But a manufacturer has to have a best-seller.

## Exercise 1

- Let us design a database for a bank, including information about customers and their accounts. Information about a customer includes their name, address, phone, and SIN number. Accounts have numbers, types (e.g., savings, checking) and balances. We also need to record the customer(s) who own an account. Draw the E/R diagram for this database.
- Modify your solution as follows: 
  - a) Change your diagram so an account can have only one customer. 
  - b) Change your diagram so that a customer can have a set of addresses (which are street-city-province triples) and a set of phones. Remember that we do not allow attributes to have nonatomic types, such as sets, in the E/R model.
  - c) Further modify your diagram so that customers can have a set of addresses, and at each address there is a set of phones.

## Exercise 2

- Give an E/R diagram for a database recording information about teams, players, and their fans, including: 

  1. For each team, its name, its players, its team captain (one of its players), and the colors of its uniform.

  2. For each player, his/her name. 
  3. For each fan, his/her name, favorite teams, favorite players, and favorite color.

- Suppose we wish to add to the schema a relationship “Led-by” among two players and a team. The intention is that this relationship set consists of triples
  (player1, player2, team) such that player 1 played on the team at a time when some other player 2 was the team captain. 

- Draw the modification to the E/R diagram.

# Chapter 1 - The Worlds of Database Systems

# Chapter 2 - The Relational Database Modeling

# Chapter 3 - Design Theory for Relational Databases

# Chapter 4 - High-level Database Models

# Chapter 5 - Algebraic and Logical Query Languages

# Chapter 6 - The Database Language SQL

# Chapter 7 - Constraints and triggers

# Chapter 8 - Views and Indexes

# Chapter 9 -SQL in a Server Environment

# Chapter 10 - Advanced Topics in Relational Databases

# Chapter 11 - The Semistructured-Data Model

# Chapter 12 - Programming Languages for XML

# Chapter 13 - Secondary Storage Management

# Chapter 14 - Index Structures

# Chapter 15 - Query Execution

# Chapter 16 - The Query Compiler

# Chapter 17 - Coping With System Failures

# Chapter 18 - Concurrency Control

# Chapter 19 - More Abou t Transaction Management

# Chapter 20 - Parallel and Distributed Databases

# Chapter 21 - Information Integration

# Chapter 22 - Data Mining

# Chapter 23 -  Database System s and the Internet
