# Transforming ER Diagram to Relational Model

## Objectives
- Transform the given Entity Relationship Diagram to a relational model step by step

## Instructions
1. From the given ER diagram, use 8-step transformation to create a relational model.
   Note: you must show the step-by-step transformation
2. Submit by the end of the class

Given the following ER diagram, use 8-step transformation to create a relational model, including:

1. Transform regular entities including simple and composite attributes
2. Transform weak entities
3. Transform binary 1:1 relationship
4. Transform binary 1:M relationship
5. Transform binary M:N relationship
6. Transform multivalued attributes
7. Transform N-ary relationship
8. Transform specialization or generalization

***Note***: If some steps are not applicable, i.e., no such entities, attributes, or relationships in the ERD, please specify "**Not applicable**"

## Step-by-Step Transformation

### 1. Transform regular entities including simple and composite attributes

```mermaid
erDiagram
    A {
        int id PK
        string a1
        string a2
        string a31
        string a32
        string a33
        string a4
    }
    B {
        int id PK
        string b1
        string b2
        string b4
    }
    C {
        int id PK
        string c1
        string c2
        string ctype
    }
    D {
        int id PK
        string d1
        string d2
        string d3
    }
    E {
        int id PK
        string e1
        string e2
        string e3
    }
    F {
        int id PK
        string f1
        string f2
    }
    G {
        int id PK
        string g1
        string g2
    }
```

Explanation:
- Entities A, B, C, D, E, F, and G are transformed into separate tables
- All attributes are converted into columns in their respective tables
- The composite attribute a3 of entity A is broken down into sub-columns (a31, a32, a33)
- Optional attributes (b3, c3) are not included as they are represented by dashed lines in the original diagram

### 2. Transform weak entities

**Not applicable** - There are no weak entities in this diagram

### 3. Transform binary 1:1 relationship

```mermaid
erDiagram
    A {
        int id PK
        string a1
        string a2
        string a31
        string a32
        string a33
        string a4
    }
    B {
        int id PK
        string b1
        string b2
        string b4
        int a_id FK
    }
    A ||--|| B : "rAB"
```

Explanation:
- The 1:1 relationship (rAB) between A and B is transformed by adding a foreign key (a_id) in table B
- We choose to add the foreign key in table B as this relationship might be optional from B to A

### 4. Transform binary 1:M relationship

```mermaid
erDiagram
    A {
        int id PK
        string a1
        string a2
        string a31
        string a32
        string a33
        string a4
    }
    B {
        int id PK
        string b1
        string b2
        string b4
        int a_id FK
        int parent_b_id FK
    }
    C {
        int id PK
        string c1
        string c2
        string ctype
        int a_id FK
    }
    D {
        int id PK
        string d1
        string d2
        string d3
    }
    G {
        int id PK
        string g1
        string g2
        int d_id FK
    }
    A ||--o{ B : "rAB"
    A ||--o{ C : "rAC"
    B ||--o{ B : "rBB"
    D ||--o{ G : "rDG"
```

Explanation:
- The 1:M relationship (rAC) between A and C is transformed by adding a foreign key (a_id) in table C
- The recursive 1:M relationship (rBB) in table B is transformed by adding a foreign key (parent_b_id) referencing itself
- The 1:M relationship (rDG) between D and G is transformed by adding a foreign key (d_id) in table G

### 5. Transform binary M:N relationship

```mermaid
erDiagram
    C {
        int id PK
        string c1
        string c2
        string ctype
    }
    D {
        int id PK
        string d1
        string d2
        string d3
    }
    CD {
        int c_id FK
        int d_id FK
        string cd1
    }
    C ||--o{ CD : ""
    D ||--o{ CD : ""
```

Explanation:
- The M:N relationship (rCD) between C and D is transformed by creating a new table CD
- Table CD has foreign keys (c_id and d_id) referencing tables C and D respectively
- The relationship attribute (cd1) is added to the CD table

### 6. Transform multivalued attributes

**Not applicable** - There are no multivalued attributes in this diagram

### 7. Transform N-ary relationship

```mermaid
erDiagram
    D {
        int id PK
        string d1
        string d2
        string d3
    }
    E {
        int id PK
        string e1
        string e2
        string e3
    }
    F {
        int id PK
        string f1
        string f2
    }
    DEF {
        int d_id FK
        int e_id FK
        int f_id FK
        string def1
    }
    D ||--o{ DEF : ""
    E ||--o{ DEF : ""
    F ||--o{ DEF : ""
```

Explanation:
- The N-ary relationship (rDEF) between D, E, and F is transformed by creating a new table DEF
- Table DEF has foreign keys (d_id, e_id, and f_id) referencing tables D, E, and F respectively
- The relationship attribute (def1) is added to the DEF table

### 8. Transform specialization or generalization

```mermaid
erDiagram
    C {
        int id PK
        string c1
        string c2
        string ctype
    }
    subC1 {
        int c_id FK
        string sc11
        string sc12
    }
    subC2 {
        int c_id FK
        string sc21
        string sc22
    }
    subC3 {
        int c_id FK
        string sc31
        string sc32
    }
    C ||--o{ subC1 : ""
    C ||--o{ subC2 : ""
    C ||--o{ subC3 : ""
```

Explanation:
- The specialization of entity C into subC1, subC2, and subC3 is transformed using the Multiple Table Inheritance approach
- Separate tables are created for each subclass (subC1, subC2, subC3)
- Each subclass table has a foreign key (c_id) referencing table C
- Specific attributes of each subclass are stored in their respective subclass tables
- The ctype in table C may be used as a discriminator to indicate the type of subclass
