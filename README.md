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

## Keys

- A key (for an entity set) is a set of attributes such that no two entities are the same on all the attributes of the key.
- In Entity-Relationship, we underline the key attribute(s).

![image-20230127133829760](assets/image-20230127133829760.png)

![image-20230127133916963](assets/image-20230127133916963.png)

## Keys for Movies

- Let’s consider the entity set **Movie**.
- We might assume that the attribute title is a key. However, there can be different movies with the same name:
  - “Godzilla” has several different versions (Japanese, American etc.).
- If we **enforce** in the database a **key constraint** on attribute **title** of **Movie** class, then the DBMS will not allow us to insert information about different “Godzilla’s”.
- A better choice is to take the set {title, year} of attributes as a key.
  - We still run the risk that there are two movies made in the same year, with the same title, but that’s very unlikely.

## Keys for Studios and Stars

- For **Studios**:
  - Reasonable to assume that there are no two studios having the **same name**.
  - So, we will enforce **name** to serve as a **key**.
- For **Stars**:
  - We may think that the name can’t serve to distinguish two people, but…
  - Yes! For stars the name distinguishes them since traditionally they choose “stage names”.
  - So, again here, we will enforce **name** to serve as a **key.**

## Surrogate Keys

- Often, people introduce attributes whose role is to serve as a key for classes. 
  - Companies assign employee ID’s to all employees, and these ID’s are carefully chosen to be unique numbers.
  - In Canada everyone has a SIN. 
  - Students ID’s in universities
  - Driver’s license numbers
  - Automobile registration numbers

## Entity Sets Versus Attributes I

> Example: (Bad Design)
>
> ![image-20230127134634380](assets/image-20230127134634380.png)
>
> 1. Repeats the manufacturer’s address once for each beer; 
> 2. Loses the address if there are temporarily no beers for a manufacturer.

## Entity Sets Versus Attributes II

- An entity set should satisfy at least one of the following conditions:
  - It is more than the name of something; it has at least one nonkey attribute.
  - It is the “many” in a many-one or many-many relationship.

> Example: (Good Design)
>
> ![image-20230127134805103](assets/image-20230127134805103.png)
>
> - Manfs deserves to be an entity set because of the nonkey attribute addr.
> - Beers deserves to be an entity set because it is the “many” of the many-one relationship ManfBy.

## Subclasses

- Sometimes, a class (entity set) contains certain objects (entities) that have special properties not associated with all members of the class.

![image-20230127134950426](assets/image-20230127134950426.png)

## Inheritance in the Entity-Relationship Model

- E/R entities have components in all subclasses to which they belong.

> Example: 
>
> Roger Rabit, which is both a <u>cartoon</u> and <u>murder-mystery</u>
>
> - will have components in all three entity sets: **Movies**, **Cartoons**, **Murder-Mysteries**.
> - i.e. it will have all four attributes of **Movies**, the attribute **weapon**, and finally will participate in the relationship **voices**.
>
> ![image-20230127135354873](assets/image-20230127135354873.png)

## Keys for entity set Hierarchies

- **Key of root is key for all.**
  - Ex. **{title,year}** is the key for **Movies**, **Cartoons** and **Murder-Mysteries**.

![image-20230127135520415](assets/image-20230127135520415.png)

## Weak Entity Sets

- Occasionally, entities of an entity set need “help” to identify them uniquely.
- Entity set E is said to be weak if:
  - in order to identify entities of E uniquely, we need to follow one or more many-one relationships from E and include the key of the related entities from the connected entity sets.

> Example: Weak Entity Sets
>
> - **name** is almost a key for **football players**, but there might be two with the same name.
> - **number** is certainly not a key, since players on two teams could have the same number.
> - But **number**, together with the team **name** related to the player by **Plays-on** should be unique.

## In Entity-Relationship Diagrams

![image-20230127135820647](assets/image-20230127135820647.png)

- Double diamond for **supporting** many-one relationship.
- Double rectangle for the weak entity set.

## Weak Entity-Set Rules

- A weak entity set has one or more many-one relationships to other
  (supporting) entity sets.
  - Not every many-one relationship from a weak entity set need be supporting.
  - But supporting relationships must have a rounded arrow (entity at the “one” end is guaranteed).
- The key for a weak entity set is its own underlined attributes and the keys for the supporting entity sets.
  - E.g., (player) **number** and (team) **name** is a key for **Players** in the previous example.

# From Entity-Relationship Diagrams to Relations

![image-20230127140305083](assets/image-20230127140305083.png)

## Relations (or Tables) Terminology

![image-20230127140343559](assets/image-20230127140343559.png)

## Terminology

Every attribute has an atomic type.

- **Relation Schema:** relation name + attribute names + attribute types
- **Relation instance:** a set of tuples. Only one copy of any tuple! 
- **Database Schema:** a set of relation schemas. 
- **Database instance**: a relation instance for every relation in the schema.

## From Entity-Relationship Diagrams to Relations

- **Entity sets** become relations with the same set of attributes.
- **Many-Many Relationships** become relations whose attributes are only:
  -  The keys of the connected entity sets.
  - Attributes of the relationship itself.
  - Sometimes attribute renaming needed to avoid name clashes.
- **Many-One Relationships** usually don’t need separate tables.
  - The key of the “one” side is included in the relation of the “many” side
- **One-One Relationships** are similar.
- **Ternary (or higher) relationships** need separate tables with keys of the participating entity sets. 
  - The key is the union of keys of the “many” sides.

#### Example 1: Entity Sets to Relations

![image-20230127141019476](assets/image-20230127141019476.png)

#### Example 2: With Attribute Renaming

![image-20230127141131719](assets/image-20230127141131719.png)

#### Example 3

![image-20230127141152510](assets/image-20230127141152510.png)

#### Example 4

![image-20230127141249196](assets/image-20230127141249196.png)

## Handling Weak Entity Sets

- Relation for a weak entity set must include attributes for its complete key (including those belonging to other entity sets), as well as its own, nonkey attributes.
- A supporting (double-diamond) relationship is redundant and yields no relation.

#### Example 1

![image-20230127141601499](assets/image-20230127141601499.png)

#### Example 2

![image-20230127141727036](assets/image-20230127141727036.png)

#### Example 3

![image-20230127141743337](assets/image-20230127141743337.png)

#### Example 4

![image-20230127141808194](assets/image-20230127141808194.png)

#### Example 5 ("Isa")

![image-20230127141844666](assets/image-20230127141844666.png)

## The 00 Approach

- Every subclass has its own relation.
  - All the properties of that subclass, including all its inherited properties, are represented in this relation.

> Example:
>
> Movies( title, year, length, filmType ) 
>
> Cartoons( title, year, length, filmType ) 
>
> MurderMysteries( title, year, length, filmType, weapon) 
>
> Cartoon-MurderMysteries( title, year, length, filmType, weapon) 
>
> Voices( title, year, starName )

- Can we merge Cartoons with Movies?
  - If we do, we lose information about which moves are cartoons.

## Entity-Relationship Approach

- We will have the following relations:
  - Movies(title, year, length, filmType).
  - MurderMystery(title, year, weapon).
  - Cartoons(title, year).
  - Voices(title, year, name).

## Entity-Relationship approach - Remarks

- No relation for class Cartoon-MurderMystery.
- For a movie that is both, we obtain:
  - its voices from the Voices relation
  - its weapon from the MurderMystery relation
  - and all other information from the Movies relation.
- Relation Cartoons has a schema that is a subset of the schema for the relation Voices. *Should we eliminate the relation Cartoons?*
- However there may be **silent** cartoons in our database. Those cartoons would have no voices and we would lose them.

## Comparison of Approaches

#### OO translation drawback:

- Too many tables! Why?
  - In the OO approach if we have a root and n children we need 2^n different tables!!!

#### E/R translation drawback: 

 We may have to look in several relations to gather information about a single object.

- For example, if we want the length and weapon used for a murder mystery film, we have to look at Movies and MurderMysteries relations.

#### OO translation advantage: 

- The OO translation keeps all properties of an object together in one relation.

#### E/R translation advantage: 

- The E/R translation allows us to find in one relation tuples from all classes in the hierarchy.

##### Comparison Examples

- <u>What movies of 2009 were longer than 150 minutes?</u>
  - Can be answered directly in the E/R approach.
  - In the OO approach we have to examine all the relations.
- <u>What weapons were used in cartoons of over 150 minutes in length?</u>
  - More difficult in the E/R approach. 
    - We should access Movies to find those of over 150 mins.
    - Then, we have to access Cartoons to see if they are cartoons.
    - Then we should access MurderMysteries to find the weapon.
  - In OO approach we need only access the Cartoon-MyrderMysteries table.

## Null Values to Combine Relations

- If we are **allowed** to use **NULL** in tuples, we can handle a hierarchy of classes with a single relation.
  - This relation has attributes for all the properties possessed by objects in any of the classes of the hierarchy.
  - An object is represented by a single tuple. This tuple has NULL in each attribute corresponding to a property that does not belong to the object’s class.
- If we apply this approach to the Movie hierarchy, we would create a single relation whose schema is:
  - **Movie**(title, year, length, filmType, studioName, starName, voice, weapon) 
    - “Who Framed Roger Rabbit?”, being both a cartoon and a murder-mystery, would be represented by several tuples that had no NULL’s.
    - The Little Mermaid, being a cartoon but not a murder-mystery, would have NULL in the weapon component.
- This approach allows us to find **all** the information about an object in one relation. Drawback?
  - Depending on the data, there could be too many nulls.

# SQL 

## Create Table

```sql
CREATE TABLE Studios( name VARCHAR(20), website VARCHAR(255));

CREATE TABLE Stars ( name VARCHAR(20), gender CHAR(1), birthyear INT, birthplace VARCHAR(40));

CREATE TABLE Movies ( title VARCHAR(50), year INT, length INT, rating CHAR(2), studioname VARCHAR(20));

CREATE TABLE StarsIn ( title VARCHAR(50), year INT, starname VARCHAR(20));
```

## CHAR and VARCHAR

- **CHAR(n)** allocates a fixed space, and if the string that we store is shorter than **n**, then it is padded with blanks.
- Differently, **VARCHAR(n)** denotes a string of up to **n** characters.
  - VARCHAR(n) allows for compression to save space.
- Use CHAR(n) for frequently used fields, and use VARCHAR(n) otherwise.

## Insert - Studios

```sql
INSERT INTO Studios 
VALUES('Fox', 'foxmovies.com');

INSERT INTO Studios 
VALUES('Disney', 'disney.com');

INSERT INTO Studios 
VALUES('Paramount', 'www.paramount.com');
```

## Insert - Movies

```sql
INSERT INTO Movies 
VALUES('Walk the Line', 2005, 136, 'PG', 'Fox');

INSERT INTO Movies 
VALUES('Pretty Woman', 1990, 119, 'R', 'Disney');

INSERT INTO Movies 
VALUES('Wayne''s World', 1991, 104, 'PG', 'Paramount');

INSERT INTO Movies 
VALUES('Unfaithful', 2002, 124, 'R', 'Fox');

INSERT INTO Movies 
VALUES('Runaway Bride', 1999, 116, 'PG', 'Paramount');

INSERT INTO Movies 
VALUES('The Princess and the Frog', 2009, 97, 'G', 'Disney');
```

## Insert - Stars

```sql
INSERT INTO Stars 
VALUES('Richard Gere', 'M', 1949, 'Philadelphia, Pennsylvania, USA');

INSERT INTO Stars 
VALUES('Joaquin Phoenix', 'M', 1974, 'San Juan, Puerto Rico');

INSERT INTO Stars 
VALUES('Reese Witherspoon', 'F', 1976, 'Baton Rouge, Louisiana, USA');

INSERT INTO Stars 
VALUES('Julia Roberts', 'F', 1967, 'Smyrna, Georgia, USA');

INSERT INTO Stars 
VALUES('Mike Myers', 'M', 1963, 'Scarborough, Ontario, Canada');

INSERT INTO Stars 
VALUES('Oprah Winfrey', 'F', 1954, 'Kosciusko, Mississippi, USA');
```

## Insert - StarsIn

```sql
INSERT INTO StarsIn 
VALUES('Walk the Line', 2005, 'Joaquin Phoenix'); 

INSERT INTO StarsIn 
VALUES('Walk the Line', 2005, 'Reese Witherspoon');

INSERT INTO StarsIn 
VALUES('Pretty Woman', 1990, 'Richard Gere'); 

INSERT INTO StarsIn 
VALUES('Pretty Woman', 1990, 'Julia Roberts');

INSERT INTO StarsIn 
VALUES('Wayne''s World', 1991, 'Mike Myers');

INSERT INTO StarsIn 
VALUES('Unfaithful', 2002, 'Richard Gere');

INSERT INTO StarsIn 
VALUES('Runaway Bride', 1999, 'Richard Gere');

INSERT INTO StarsIn 
VALUES('Runaway Bride', 1999, 'Julia Roberts'); 

INSERT INTO StarsIn 
VALUES('The Princess and the Frog', 2009, 'Oprah Winfrey');
```

## Create Table with Primary Keys

```sql
CREATE TABLE Studios(
    name VARCHAR(20) PRIMARY KEY, 
    website VARCHAR(255)
);

CREATE TABLE Stars (
    name VARCHAR(20) PRIMARY KEY, 
    gender CHAR(1), 
    birthyear INT, 
    birthplace VARCHAR(40)
);

CREATE TABLE Movies ( 
    title VARCHAR(50), 
    year INT, 
    length INT, 
    rating CHAR(2), 
    studioname VARCHAR(20), 
    PRIMARY KEY (title, year)
);

CREATE TABLE StarsIn (
    title VARCHAR(50), 
    year INT, 
    starname VARCHAR(20), 
    PRIMARY KEY (title,year,starname)
);


```

## Create Table with Foreign Keys

```sql
CREATE TABLE Studios(
    name VARCHAR(20) PRIMARY KEY, 
    website VARCHAR(255)
);

CREATE TABLE Stars (
    name VARCHAR(20) PRIMARY KEY, 
    gender CHAR(1), 
    birthyear INT, 
    birthplace VARCHAR(40)
);

CREATE TABLE Movies (
    title VARCHAR(50), 
    year INT, 
    length INT, 
    rating CHAR(2), 
    studioname VARCHAR(20), 
    PRIMARY KEY (title, year), 
    FOREIGN KEY (studioName) REFERENCES Studios(name) ON DELETE CASCADE
);

CREATE TABLE StarsIn (
    title VARCHAR(50), 
    year INT, 
    starname VARCHAR(20), 
    PRIMARY KEY (title,year,starname), 
    FOREIGN KEY (title,year) REFERENCES Movies(title,year) ON DELETE CASCADE, 
    FOREIGN KEY (starName) REFERENCES Stars(name) ON DELETE CASCADE
);
```

## Short Form for Single Att. Foreign Keys

```sql
CREATE TABLE Movies (
    title VARCHAR(50), 
    year INT, 
    length INT, 
    rating CHAR(2), 
    studioname VARCHAR(20) REFERENCES Studios(name) ON DELETE CASCADE, 
    PRIMARY KEY (title, year)
);
```

- No need to say Foreign Key

## Creation and insertion order

1. Movies after Studios
2. StarsIn after Movies and Stars

## Dropping Tables

```sql
DROP TABLE StarsIn; 

DROP TABLE Movies; 

DROP TABLE Stars; 

DROP TABLE Studios;
```

> Note: Order of drops is important if foreign key constraints are in place.

## Getting all the tuples of a table

```SQL
SELECT * FROM Movies;
```

## Altering Table Structure

```sql
ALTER TABLE Stars ADD phone CHAR(7); 

ALTER TABLE Stars MODIFY phone CHAR(10); 

ALTER TABLE Stars DROP COLUMN phone;
```

# Relational Algebra

## Operations in the Relational Model

- These operation can be expressed in an algebra, called **“relational algebra.”**
- In this algebra, **relations** are the **operands** and we apply **operators** on them.

## Operations

Four Broad classes:

#### Usual set opperations

- **Union**
- **Intersection**
- **Difference**

#### Operations that remove parts of a relation:

- **Selection** - eliminates some rows(tuples)
- **Projection** - eliminates some columns

#### Operations that combine the tuples of two relations:

- **Cartesian Product** - pairs tuples of two relations in all possible ways
- **Join** - selectively pairs tuples from two relations

#### An operation called **“renaming”**

## Conditions for Set Operations on Relations

We can apply union, intersection, difference- on relations R and S provided that:

1. **R** and **S** must have schemas with identical sets of attributes.
2. Before applying the operations, the columns of **R** and **S** must be ordered so that the order of attributes is the same for both relations.

## Set Operations on Relations

| Operation                                                    | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![image-20230127150958362](assets/image-20230127150958362.png) | the **union** of **R** and **S**, is the set of tuples that are in **R** or **S** or both |
| ![image-20230127151009749](assets/image-20230127151009749.png) | the **intersection** of **R** and **S**, is the set of tuples that are in both **R** and **S**. |
| ![image-20230127151020227](assets/image-20230127151020227.png) | the **difference** of **R** and **S**, is the set of tuples that are in **R** but not in **S**. |

> Note:  that R -  S is different from S - R.

## Projection

| Operation                                                    | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![image-20230127151237942](assets/image-20230127151237942.png) | Produces from relation **R** a new relation that has only the A1, …, An columns of **R**. |

#### Example

![image-20230127151307478](assets/image-20230127151307478.png)

| Title        | Year | Length | FilmType | Studioname | Producer# |
| ------------ | ---- | ------ | -------- | ---------- | --------- |
| Star wars    | 1977 | 124    | color    | Fox        | 12345     |
| Mighty Ducks | 1991 | 104    | color    | Disney     | 67890     |
| Waynes world | 1992 | 95     | color    | Paramount  | 99999     |

We get:

| Title        | Year | Length |
| ------------ | ---- | ------ |
| Star wars    | 1977 | 124    |
| Mighty Ducks | 1991 | 104    |
| Waynes World | 1992 | 95     |

## Selection

| Operation                                                    | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![image-20230127151930224](assets/image-20230127151930224.png) | Produces a new relation with those tuples of R which satisfy condition C. |

#### Example 1

![image-20230127151959402](assets/image-20230127151959402.png)

| Title        | Year | Length | Filmtype | Studioname | Producer# |
| ------------ | ---- | ------ | -------- | ---------- | --------- |
| Star Wars    | 1977 | 124    | color    | Fox        | 12345     |
| Mighty Ducks | 1991 | 104    | color    | Disney     | 67890     |

#### Example 2

Suppose we want the movies by Fox which are at least 100 minutes long.

![image-20230127152235110](assets/image-20230127152235110.png)

Results in:

| Title     | Year | Length | Filmtype | Studioname | Producer# |
| --------- | ---- | ------ | -------- | ---------- | --------- |
| Star Wars | 1977 | 124    | color    | Fox        | 12345     |

## Cartesian Product

| Operation                                                    | Description |
| ------------------------------------------------------------ | ----------- |
| ![image-20230127152526118](assets/image-20230127152526118.png) | See below   |

1. Set of tuples **rs** that are formed by choosing the first part (**r**) to be any tuple of **R** and the second part (**s**) to be any tuple of **S**
2. Schema for the resulting relation is the union of schemas for **R** and **S**.
3. If **R** and **S** happen to have some attributes in common, then prefix those attributes by the relation name.

#### Example

R = 

| A    | B    |
| ---- | ---- |
| 1    | 2    |
| 3    | 4    |

S = 

| A    | C    | D    |
| ---- | ---- | ---- |
| 2    | 5    | 6    |
| 4    | 7    | 8    |
| 9    | 10   | 11   |

R x S = 

| A    | R.B  | S.B  | CD   | D    |
| ---- | ---- | ---- | ---- | ---- |
| 1    | 2    | 2    | 5    | 6    |
| 1    | 2    | 4    | 7    | 8    |
| 1    | 2    | 9    | 10   | 11   |
| 3    | 4    | 2    | 5    | 6    |
| 3    | 4    | 4    | 7    | 8    |
| 3    | 4    | 9    | 10   | 11   |



## Theta-Join

![image-20230127153555837](assets/image-20230127153555837.png)

- The result of this operation is constructed as follows: 

  - a) Take the Cartesian product of **R** and **S**.
  - b) Select from the product only those tuples that satisfy the condition **C**.

- Schema for the result is the union of the schema of **R** and **S** with, “**R**” or “**S**” prefix as necessary.

  

  When the condition is equality, we call it “equijoin”.

## Natural Join

![image-20230127153726900](assets/image-20230127153726900.png)

- Let **A1, A2,…,An** be the attributes in both the schema of **R** and the schema of **S**.
- Then a tuple **r** from **R** and a tuple **s** from **S** are successfully paired if and only if **r** and **s** agree on each of the attributes **A1, A2, …, An.**

#### Example

The natural join of the relation R and S from previous example is:

| A    | B    | C    | D    |
| ---- | ---- | ---- | ---- |
| 1    | 2    | 5    | 6    |
| 3    | 4    | 7    | 8    |

![image-20230127153931197](assets/image-20230127153931197.png)

![image-20230127153946101](assets/image-20230127153946101.png)

## Combing Operations to Form Queries

#### Example 1

Question: “What are the title and years of movies made by Fox that are at least 100 minutes long?”

![image-20230127154213308](assets/image-20230127154213308.png)

```sql
SELECT title, year 
FROM Movies 
WHERE length>=100 AND studioName=‘Fox’;
```

#### Example 2

Question: 

- Consider two relations Movies and StarsIn

- With schemas: 
  - Movies(title, year, length, filmType, studioName) 
  - StarsIn(title, year, starName)
- Suppose we want to know: 
  - “Find the stars of the movies that are at least 100 minutes long.”

> Note: 
>
> First we join the two relations: Movies, StarsIn 
>
> Second we select movies with length at least 100 min. 
>
> Then we project onto starName.

![image-20230127154409712](assets/image-20230127154409712.png)

```sql
SELECT starName 
FROM Movies, StarsIn 
WHERE Movies.title=StarsIn.title 
AND Movies.year=StarsIn.year 
AND length>=100;
```

#### Example 2 (Alternative Solution 1)

<img src="assets/image-20230127154518310.png" alt="image-20230127154518310"  />

```sql
SELECT starName
FROM Movies 
JOIN StarsIn 
ON Movies.title=StarsIn.title 
AND Movies.year=StarsIn.year
WHERE length>=100;
```

#### Example 2 (Alternative Solution 2)

![image-20230127154616346](assets/image-20230127154616346.png)

```sql
SELECT starName 
FROM Movies 
JOIN StarsIn 
USING (title, year) 
WHERE length>=100;
```

OR (Less safe)

```sql
SELECT starName 
FROM Movies 
NATURAL JOIN StarsIn 
WHERE length>=100;
```



## Renaming Operator

![image-20230127154733032](assets/image-20230127154733032.png)

- Resulting relation has exactly the same tuples as **R**, but the name of the relation is **S**.
- Moreover, the attributes of the result relation **S** are named **A1, A2, …, An,** in order from the left.

#### Problem

Product(maker, model, type) 

PC(model, speed, ram, hd, rd, price) 

Laptop(model, speed, ram, hd, screen, price)

Printer(model, color, type, price)

![image-20230127155002689](assets/image-20230127155002689.png)

> a) Which PC models have a speed of at least 1000?
>
> b) Which manufacturers make laptops with a hard disk of at least 30?
>
> c) Find the model number and price of all products (of any type) made by manufacturer B.
>
> d) Find the model numbers of all color laser printers. 
>
> e) Find those manufacturers that sell Laptops, but not PC's. 
>
> !f) Find those hard-disk sizes that occur in two or more PC's. 
>
> !g) Find those pairs of PC models that have both the same speed and RAM. A pair should be listed once.
>
> !!h)Find those manufacturers of at least two different computers (PC or Laptops) with speed of at least 700.

# Extended Relational Algebra

## Bags

> **Bag**
>
> Is like a set, but an element may appear more than once.
>
> Note: Multiset is another name for “bag.”

Example:

- {1,2,1,3} is a bag.
- {1,2,3} is also a bag that happens to be a set.

Bags also resemble lists, but order in a bag is unimportant.

Example:

- {1,2,1} = {1,1,2} as bags, but
- [1,2,1] != [1,1,2] as lists.

## Why Bags?

- SQL is actually a bag language.
- SQL will eliminate duplicates, but usually only if you ask it to do so explicitly
  - except for **union, intersection**, and **difference** where the default is “set mode”.

> Note: Union, intersection, and difference need new definitions for bags.

## Bag Union

An element appears in the union of two bags the sum of the number of times it appears in each bag

> **Example:**
>
> {1,2,1} UNION {1,1,2,3,1} = {1,1,1,1,1,2,2,3}

## Bag Intersection

An element appears in the intersection of two bags the minimum of the number of times it appears in either.

> Example:
>
> {1,2,1} INTERSECT {1,2,3} = {1,2}.

## Bag Difference

An element appears in difference A – B of bags as many times as it appears in A, minus the number of times it appears in B.

- But never less than 0 times

> Example:
>
> {1,2,1} – {1,2,3} = {1}

## Union, Intersection, Difference in SQL

> Note: Remember, we need to have the same schema for the relations that we union, intersect, or take difference.

```sql
(SELECT * FROM R) 
UNION 
(SELECT * FROM S);

(SELECT * FROM R) 
INTERSECT 
(SELECT * FROM S);

(SELECT * FROM R) 
EXCEPT 
(SELECT * FROM S);
```

- Add “ALL” for bag version of these operators.
  - These are the only operators that work in ‘set mode’ by default.
  - All the others work in ‘bag mode’ by default.

## Extended Relational Algebra

![image-20230128144654746](assets/image-20230128144654746.png)

## Example: Duplicate Elimination

![image-20230128144731640](assets/image-20230128144731640.png)

- R1 consists of one copy of each tuple that appears in R2 one or more times.

R =

| A    | B    |
| ---- | ---- |
| 1    | 2    |
| 3    | 4    |
| 1    | 2    |

1*(R) = 

| A    | B    |
| ---- | ---- |
| 1    | 2    |
| 3    | 4    |

```SQL
SELECT DISTINCT * FROM R;
```

## Sorting

![image-20230128144939297](assets/image-20230128144939297.png)

- L is a list of some of the attributes of R_2.
- R1 is the list of tuples of R2 sorted first on the value of the first attribute on L, then on the second attribute of L, and so on.
- the only operator whose result is neither a set nor a bag, but a **list**

```sql
SELECT * FROM R ORDER BY A, B;
```

## Example: Extended Projection

![image-20230128145059285](assets/image-20230128145059285.png)

## Aggregation Operators

- They apply to entire columns of a table and produce a single result.
- Most important examples:
  - SUM
  - AVG
  - COUNT
  - MIN
  - MAX

## Example: Aggregation

R =

| A    | B    |
| ---- | ---- |
| 1    | 3    |
| 3    | 4    |
| 3    | 2    |

- SUM(A) = 7 
- COUNT(A) = 3 
- MAX(B) = 4 
- MIN(B) = 2 
- AVG(B) = 3

```SQL
SELECT SUM(A), COUNT(A), MAX(B), MIN(B), AVG(B) FROM R;
```



## Grouping Operator

![image-20230128145300082](assets/image-20230128145300082.png)

## Grouping Operator L(R) - Formally

- Group relation R according to all the grouping attributes on list L.
  - That is, form one group for each distinct list of values for those attributes in R.
- Within each group, compute AGG(A) for each aggregation on list L.
- Result has grouping attributes and aggregations as attributes.
  - One tuple for each list of values for the grouping attributes and their group’s aggregations

## Example: Grouping/Aggregation

**StarsIn(title, year, starName)**

> How many movies each star has starred in?
>
> ![image-20230128145447901](assets/image-20230128145447901.png)



> What’s the earliest year each star has starred in some movie? 
>
> ![image-20230128145456980](assets/image-20230128145456980.png)



> How many stars have starred in in each movie?
>
> ![image-20230128145507748](assets/image-20230128145507748.png)

> For each star who has appeared in at least three movies give the earliest year in which he or she appeared.
>
> ![image-20230128145625723](assets/image-20230128145625723.png)
>
> Translating the previous RA expression to SQL:
>
> ```SQL
> SELECT starName, miny 
> FROM (SELECT starname, COUNT(title) AS cnt, 
>       MIN(year) AS miny 
>       FROM StarsIn 
>       GROUP BY starname)
> WHERE cnt>=3;
> ```
>
> OR
>
> ```SQL
> SELECT starname, MIN(year) AS miny 
> FROM StarsIn 
> GROUP BY starname 
> HAVING COUNT(title)>=3;
> ```
>
> 

## Outerjoin

**Motivation** 

- Suppose we join R S.
- A tuple of R which doesn't join with any tuple of S is said to be dangling.
  - Similarly for a tuple of S.
  - **Problem**: We loose dangling tuples.

**Outerjoin** 

- Preserves dangling tuples by padding them with NULL in the result.

## Example: Outerjoin

R = 

| A    | B    |
| ---- | ---- |
| 1    | 2    |
| 4    | 5    |

S = 

| A    | C    |
| ---- | ---- |
| 2    | 3    |
| 6    | 7    |

(1,2) joins with (2,3), but the other two tuples are dangling.

R OUTRJOIN S = 

| A    | B    | C    |
| ---- | ---- | ---- |
| 1    | 2    | 3    |
| 4    | 5    | NULL |
| NULL | 6    | 7    |

```SQL
SELECT * FROM R FULL OUTER JOIN S USING(B);
```

## Exercises

![image-20230128150227383](assets/image-20230128150227383.png)

# SQL Queries (sql2)

## Select-From-Where Statements

Principal form of a query is:

```sql
SELECT desired attributes 
FROM one or more tables
WHERE condition about tuples of the tables
```

1. Begin with the relation in the FROM clause.
2. Apply the selection indicated by the WHERE clause.
3. Apply the projection indicated by the SELECT clause.

## (Extended) Projection in SQL

```SQL
SELECT title, length 
FROM Movies 
WHERE studioName = 'Disney';

SELECT title AS name, length AS duration 
FROM Movies 
WHERE studioName = 'Disney';

SELECT title AS name, length*0.016667 AS lenghtInHours 
FROM Movies 
WHERE studioName = 'Disney';

SELECT title AS name, length/60.0 AS length, 'hrs.' AS inHours
FROM Movies 
WHERE studioName = 'Disney';
```

## WHERE in SQL



## Selection in SQL

## Patterns in WHERE

## Ordering the Input

## Products and Joins in SQL

## Products and Joins in SQL

## Natural Join

## Natural Join with USING

## Join with ON

## Outer Joins

## Example

## Outerjoins: Students example (I)

## Outerjoins: Students example (II)

## Outerjoins: Students example (III)

## Outerjoins: Students example (IV)

## Outerjoins: Students example (V)

## Outerjoins: Students example (VI)

## Union/Intersection/Difference

## Aliases

## Aggregations

## Eliminating Duplicates in an Aggregation

## Not only in COUNT…

## Grouping

## Another Example

## HAVING Clauses

## Requirements on HAVING Conditions

## Restriction on SELECT Lists With Aggregation

## Illegal Query Example

## Exercise

## Correlated Subqueries

## Another Solution (Nesting in FROM)

## Views

## Accessing a View

## View on more than one relation

## EXISTS / NOT EXISTS

# NULLs in SQL (sql3)

# Database Modifications (sql4)

# Constraints (Primary Key, Unique, Foreign Key, Not Null)

# Security and Authorization

# Data Analysis with SQL



