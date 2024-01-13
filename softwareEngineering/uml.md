# Software Engineering
# Chapter 1:

# Table of Content
- [Software Engineering](#software-engineering)
- [Chapter 1:](#chapter-1)
- [Table of Content](#table-of-content)
- [Introduction to UML](#introduction-to-uml)
  - [UML - Unified Modeling Langauge](#uml---unified-modeling-langauge)
  - [Key points about UML](#key-points-about-uml)
  - [Examples for illustration](#examples-for-illustration)
- [UseCases](#usecases)
- [Activity Diagrams](#activity-diagrams)

# Introduction to UML
## UML - Unified Modeling Langauge
- **UML** stands for **Unified Modeling Language**. 
- It is a standardized modeling lanaugage used in software engineering to visualize, design, specify, construct, and document software systems.
- **UML** provides a common notation that allows software developers, architects, and stakeholders to communicate and understand the various aspects of a software system's structure and behavior.

## Key points about UML
|Key Point|Details|
|-|-|
Visual Modeling Language| UML uses a diagram and visual representation to depict different aspects of a software system. It offers various diagram types, including class diagrams, use case diagrams, sequence diagrams, activity diagrams, and more, each focusing on different aspects of the system.
Standarized Notation|UML provides a standardized and consistent way to represent the different elements of a software system. For instance, classes, objects, relationships between objects, behaviors, and interactions among system components are all represeneted using standardized symbols and notations.
Communication Tool| UML acts as a common language for software developers and stakeholders, facilitating communication and collaboration among team members. It helps in conveying complex system structures and behaviors in a more understandable and organized manner.
Supports Software Design| UML is used throughout the software development lifecycle. It aids in the initial phases of requirement analysis and system design, and it continues to be useful during implementation, testing, and maintenance of software systems.
Adaptability and Extensibility| UML is adaptable and extensible, allowing it to be tailored to specific projects or domains. It can be extended with profiles and stereotypes to fit the needs of different software development methodologies or specialized domains.

## Examples for illustration
Consider a simple scenario of a libarary system, we want to represent the classess and their relationships involved in this system.

Using **Class Diagram**:

```plaintext
-------------------------------------
|            Library                |
-------------------------------------
| - name: String                   |
| - location: String               |
-------------------------------------
| + setName(name: String): void    |
| + setLocation(location: String): void |
| + getName(): String              |
| + getLocation(): String          |
-------------------------------------

-------------------------------------
|            Book                   |
-------------------------------------
| - title: String                  |
| - author: String                 |
| - isbn: String                   |
-------------------------------------
| + setTitle(title: String): void  |
| + setAuthor(author: String): void|
| + setIsbn(isbn: String): void    |
| + getTitle(): String             |
| + getAuthor(): String            |
| + getIsbn(): String              |
-------------------------------------
```

In this example:
- There are two classes: Library and Book.
- Each class has attributes (enclosed in the top section) and methods (listed below the attributes).

Relationships:
- There can be a one-to-many relationship between Library and Book, indicating that one library can have multiple books. This relationship is represented with associations in UML.

Diagram Notation:
- The boxes represent classes.
- Attributes are listed within the class box.
- Methods are listed below the attributes.
- + indicates public methods or attributes.
- - indicates private methods or attributes.

This is a basic representation, but UML can be much more complex and detailed depending on the system being modeled. It's a visual way to represent the structure and behavior of a system, making it easier to understand its components and interactions.


# UseCases

# Activity Diagrams
