# Software Engineering
# Chapter 1:

# Table of Content
- [Software Engineering](#software-engineering)
- [Chapter 1:](#chapter-1)
- [Table of Content](#table-of-content)
- [Recap](#recap)
- [Introduction to UML](#introduction-to-uml)
  - [UML - Unified Modeling Langauge](#uml---unified-modeling-langauge)
  - [Key points about UML](#key-points-about-uml)
  - [Examples for illustration](#examples-for-illustration)
- [Use case](#use-case)
  - [Use Case Specification](#use-case-specification)
  - [Use Case Activity Diagram](#use-case-activity-diagram)
  - [Components/Concepts of Use-Case Diagram](#componentsconcepts-of-use-case-diagram)
  - [Usage](#usage)
- [UML Diagrams](#uml-diagrams)
  - [Class Diagram](#class-diagram)
  - [User Story](#user-story)
  - [Used to](#used-to)
  - [Template](#template)
    - [Components](#components)
    - [Example](#example)
    - [Release Plan](#release-plan)
    - [User Story vs Use Case](#user-story-vs-use-case)
  - [Sequence Diagrams](#sequence-diagrams)
  - [Communication Diagrams](#communication-diagrams)
  - [](#)

# Recap
let's recap the different between analysis & design
|Scope|Details|
|-|-|
Analysis|- The "WHAT"</br>- Define problem space</br>- Facilitate understanding model</br>- Unaffected by software & Perfromance considerations
Design|- The "HOW"</br>- Define solution space</br>- Model to facilitate implementation</br>- Improving performance & software

So what is objective of this recap?
- We will start to learn about the Unified Modeling Language "UML" in the rest of this chapter. The UML has some major benefits, the first of them all is that it is the unified modeling language for analysis & design.

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


# Use case
## Use Case Specification

The use-case specification could be converted to an activity diagram, and reverse is applicable.

## Use Case Activity Diagram
- Type of UML Behaviour Diagram, that visually represents the intersections between different actores and a system under consideration.
- Provides a high-level view of how a system's functionalities or features will be used by various actors.

![Use-Case Diagram](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1d/Use_case_restaurant_model.svg/1024px-Use_case_restaurant_model.svg.png)

## Components/Concepts of Use-Case Diagram
|Component|Description|
|-|-|
Actors|Represent external entities that interact with the system.</br>They can be individuals groups, or other systems that use the services provided by the system being modeled.
Use Cases|Represent specific functionalities or features of the system that provide value to one or more actors.</br>Each use case describes a particular interaction scenario between an actor and the system.
Association (Lines)|Connect actors with use cases, indicating that the actors are involved in the corresponding use cases.</br>These lines typically have arrors pointing towards the use cases to show the direction of interaction.
Include & Extend Relationships|Include relationships indicate that one use case includes the behavior of another use case.</br>Extend relationships indicate that one use case can extend the behavior of another use case under certain conditions.
System BoundaryA rectangle or boundary represents the system under consideration. </br>This use cases and actors are placed within this boundary to show their relevance to the systems.

## Usage
- Understanding system functionality
- Communication between stakeholders.
- Requirments Analysis


# UML Diagrams
There are three types of diagrams defined in UML, which are:
- Structure Diagram: [Class, Component, Composite] diagrams.
- Behaviour Diagram: [Activity, use case, state] diagrams.
- Interaction Diagram: [Sequence, Communication, Timing, Interaction] diagrams.

## Class Diagram

## User Story
The user stories are a fundamental concept in agile development methadologies, particularly in Scrum. They are a way to express requirements from an end-user perspective.
- User stories are simple, concise descriptions of a feature, told from the perspective of the person who desires the new capability, usually a user or a customer.
## Used to
- Used to estimate the required amount of work.
- Used to create acceptance tests.
## Template
A user story typically follows a specific template:
```
As a [type of user], I want [an action] so that [benefit/value]
```
### Components
1. Role or Persona (As a [type of user]): Describes the type of user or stakeholder who will benefit from the feature.
2. Action (I want [an action]): Describes the functionality or action that the user desires.
3. Benefit or Value (So that [benefit/value]): Specifies the reason or the value the user gains from the desired action.
### Example
"As a website visitor, I want to easily reset my password so that I can regain access to my acount"
- Role or Persona: Website Visitor
- Action: Resetting the password
- Benefit or Value: Regaining access to the account
### Release Plan
**The release plan determines which stories will be available in which release**.

It provides a strategic overview of the scope and timing of upcoming release, helping the development team, product owner, stackholders understand when specific features of functionalities will be delivered to users.

### User Story vs Use Case
In summary:
- Use Case:
  - High level of details
  - High level of specification
- User Story:
  - Low level of details
  - Low level of specification
  
Aspect	|User Story	|Use Case
|-|-|-|
Definition|	Brief, informal description of a feature from a user's perspective.|	A detailed description of a specific interaction within the system.
Scope|	Typically represents a small, single functionality or feature.|	Can cover a broader range of functionalities or interactions.
Format|	Follows a simple template: "As a [user], I want [feature] so that [benefit]."|	Often written in a more structured and formalized format.
Perspective|	Emphasizes the user's needs and goals.|	Focuses on the interaction between an actor and the system.
Granularity|	Generally smaller in scope, often focused on individual tasks.|	Can be more extensive, covering a sequence of interactions.
Flexibility|	Agile and adaptable, allowing for changes during development.|	Can be less flexible, as changes may require updates to the entire use case.
Commonly Used In|	Commonly used in agile methodologies like Scrum.|	Often associated with traditional methodologies like Unified Process.
Documentation Level|	Lightweight documentation; serves as a placeholder for a conversation.|	Detailed documentation with steps, conditions, and variations.
Iterations|	Typically used iteratively, with room for evolving requirements.|	May be more static and finalized early in the development process.
Common Artifacts|	Often tracked on a physical or digital board using user story cards.|	Can be represented in use case diagrams and detailed use case specifications.
Communication|	Promotes communication and collaboration between stakeholders.|	Can serve as a comprehensive communication tool between various roles.
Dependency Management|	Easy to manage dependencies with other user stories.	|Dependencies may be more complex, especially in large-scale systems.
Testing Focus	|Encourages testing from the user's perspective.|	Guides testing toward specific scenarios and system interactions.

## Sequence Diagrams
## Communication Diagrams
##