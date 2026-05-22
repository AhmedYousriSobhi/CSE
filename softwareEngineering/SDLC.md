# Software Development Life Cycle (SDLC)
# Table of Content
- [Software Development Life Cycle (SDLC)](#software-development-life-cycle-sdlc)
- [Table of Content](#table-of-content)
- [Software Development Process](#software-development-process)
  - [Phases of Software Development Process](#phases-of-software-development-process)
    - [Deep Details](#deep-details)
- [Software Architecture Vs Software Design](#software-architecture-vs-software-design)
  - [Key Difference](#key-difference)
- [Product Line Engineering (PLE)](#product-line-engineering-ple)
- [Models](#models)
  - [Why do we need Modeling?](#why-do-we-need-modeling)
  - [Types](#types)
    - [Single-Version Models](#single-version-models)
      - [Bing-Bang Model](#bing-bang-model)
      - [Waterfall Model](#waterfall-model)
        - [Phases](#phases)
        - [Why not to use WaterFall Model?](#why-not-to-use-waterfall-model)
      - [V-Model](#v-model)
      - [Phases](#phases-1)
    - [Incremental Model](#incremental-model)
    - [Iterative Model](#iterative-model)
    - [Incremental vs Iterative Models](#incremental-vs-iterative-models)

# Software Development Process
Also known as a Software Development Life Cycle (SDLC), is a set of systematic steps of phases that guide the development of high-quality software.

The purpose of a software development process is to produce software that meets the specified requirements, is devlivered on time, and with in the budget. It provides a structured and organized approach to software development, ensuring efficiency, reliability, and maintainability of the final product.

**<span style="color:lightblue">
Software changes due to correlation, adaption, and enhancement
</span>**

## Phases of Software Development Process
1. Requirements ---o/p---> SRS "Software Requirements Specification", use cases
2. Design ---o/p---> Design document, design classes
3. Implementation ---o/p---> Code
4. Test ---o/p---> test report, change requrests
### Deep Details
|Term|Details|
|-|-|
SRS "Software Requirements Specification"| - The SRS is a detailed document that serves as a blueprint for the entire software development process. It precisely defines the functional and non-functional requirements of the software to be developed.</br>- The document outlines the system's features, capabilities, constraints, and the expected behavior under various conditions.</br>-It acts as a communication bridge between stakeholders, including clients, project managers, and development teams, ensuring a common understanding of what the software is intended to achieve.</br>-The SRS typically includes sections such as Introduction, Purpose, Scope, Definitions, System Overview, Functional Requirements, Non-functional Requirements, and more.
Use Cases|- Use cases are a specific technique for documenting and modeling the functional requirements of a system from an end-user perspective.</br>- A use case describes a specific interaction between a user (or an external entity) and the system to achieve a particular goal.</br>- Each use case typically includes a description of the flow of events, preconditions, postconditions, and any alternative paths that users might take.</br>- Use cases help in understanding how users will interact with the system and provide a basis for designing and testing specific functionalities.

# Software Architecture Vs Software Design
|Aspect|Software Architecture|Software Design
|-|-|-|
Definition|It defines the overall structure and organization of a software system, addressing high-level decisions such as the choice of components, their relationships, and how they interact. It sets the foundation for the system and influences qualities like performance, scalability, and maintainability.|It involves detailed specification of the software system, focusing on how the components identified in the architecture are implemented. It deals with lower-level decisions, including algorithms, data structures, and specific technologies.
Scope| Encompasses the entire system, emphasizing the global view of its structure and behavior.|Concentrates on the implementation details of individual components or modules.
Abstraction Level|Operates at a higher level of abstraction, defining the system's major components and their relationships without delving into specific implementation details.|Operates at a lower level of abstraction, providing detailed specifications for how each component will be built.
Focus|Focuses on addressing system-level concerns, such as scalability, security, and performance.|Focuses on component-level concerns, optimizing for factors like reusability, modularity, and maintainability.
Decisions| Involves strategic decisions that have a broad impact on the entire system and its stakeholders.|Involves tactical decisions specific to the implementation of individual components.
Timeframe|Typically established early in the software development process, often during the initial phases of system planning.|Evolves throughout the development process, with detailed design decisions made as development progresses.
Change Impact|Changes to the architecture can have a significant impact on the entire system and may require substantial effort to implement.| Changes are more localized and primarily affect the specific components being modified.

## Key Difference
|Level|Differences|
|-|-|
Architecture|- Fundamental properties</br>- Define guideline</br>-The process of creating high level structure of SW systems</br>-Converts the software characteristics into high level structure</br>- Helps to define the high level infrastructure of the SW.
Design|- Detailed Properties</br>- Creates a SW artifacts describing all units of the system</br>- Creational, strucutral & behavioral are SW design patterns</br>- Helps to implement the software.

# Product Line Engineering (PLE)
Its concept is to create and manage the processes that allow a related set of products to share engineering assets & effort to achieve an effiicient means of production.

So PLE makes creating products easier & more cost effictive.

# Models
In software engineering, a Model refers to an abstraction or representation of a system, process, or a concept. It is a simplified and structured way of expressing comples ideas, relationships or designs within the software development context.

Models can take various forms, including diagrams, charts, mathematical representations, and textual descriptions.
## Why do we need Modeling?
1. Cheaper than building real thing
2. To gain understanding before building
3. To provide common vision between user & developer
4. To manage, scope & document complexity
5. To provide clear abstraction of concepts
## Types
### Single-Version Models
#### Bing-Bang Model
The term "Bing-Bang" is sometimes used to highlight an unstructured and non-methodical approach to software development, where the entire system is developed at once, without following a specific process of methodology.

The Bing-Bang scenario:
- Developer receives problem statement
- Developer works in isolation for certain time period
- Developer delivers results
- Developer hopes client is satisfied.
  
In the context of the Bing-Bang model:
- **No Defined Process**: There is no structured process or phased approach. Instead, development activities happen in an ad-hoc manner.
- **No Incremental Releases**: Unlike incremental or iterative models, there are no intermediate or incremental releases. The entire system is developed as a single unit.
- **Limited Planning**: Planning and documentation may be minimal, and the focus is on getting the entire system developed quickly.
- **Limited Testing**: Testing activities may be delayed until the entire system is developed, leading to potential challenges in identifying and addressing defects.

#### Waterfall Model
This model is one of the classic examples of single version model. It follows a linear and sequential approach, where each phase of the SDLC is completed before moving to the next.
##### Phases
```
Requirements -> Design -> Implementation -> Test
# Finish one phase then go to the other.
```
1. **Requirements**: Gather and document the requirements for the software.
2. **Design**: Create a detailed design of the system based on the requirements.
3. **Implementation**: Develop the entire system based on the design.
4. **Testing**: Perform testing to identify and fix defects.
5. **Deployment**: Deploy the fully developed and tested software to users.
6. **Maintenance**: Provide ongoing support and maintenance.

##### Why not to use WaterFall Model?
1. Requirments are changing:
   1. Market, Technology changes
   2. Gload of Stakeholders changes
2. The design may need to change during implementation
#### V-Model
The V-Model is short for "Verification and Valication Model". This model is an extention of the Waterfall model, emphasizing the relationship between development phase and its corresponding testing phase.
#### Phases
```
1- Requirements ---require---> Acceptance Test
2- System Design ---require---> Integration Test
3- Program design ---require---> Unit Test (All code must pass unit test)
4- Implementation
```
1. **Requirements**: Define and document the requirements.
2. **Design**: Create a detailed design based on the requirements.
3. **Coding**: Implement the design, creating the software.
4. **Unit Testing**: Verify individual units or components.
5. **Integration Testing**: Verify the integration of units.
6. **System Testing**: Test the complete system against the requirements.
7. **Acceptance Testing**: Validate the system against user expectations.
8. **Deployment**: Release the software to users.
9. **Maintenance**: Provide ongoing support and maintenance.

### Incremental Model
In this model, its work concept is to divide the project into small, manageable parts called increments or increments of functionality. Each increment represents a portion of the overall system functionality.
```mathematica
    _______          _______          _______
   |       |        |       |        |       |
   |   1   | -----> |   2   | -----> |   3   |  -----> Final System
   |_______|        |_______|        |_______|

   Increment 1      Increment 2      Increment 3

```

Note: Incremental models are signle version with prototyping as sawtooth model.

### Iterative Model
On the opposite site, this model involves the repetition of cycles, with each cycle refining and enhancing the software based on feedback obtained from the previous cycle.
```mathematica
    _______          _______          _______
   |       |        |       |        |       |
   | Iter1 | -----> | Iter2 | -----> | Iter3 |  -----> Final System
   |_______|        |_______|        |_______|

   Iteration 1      Iteration 2      Iteration 3
```
### Incremental vs Iterative Models
|Aspect|Incremental Model|Iterative Model
-|-|-|
Development Process|Sequential development of increaments; each increment is developed and delivered seperately|Repetition of the entire SDLC "Software Development LifeCycle" in multiple iteration
Focus|Delivering partial but complete systems in each increment|Refining and improving the entire system with each iteration
Delivery|Partial systems delivered at the end of each increment|Updated version of the entire system delivered at the end of each iteration
Testing|Incremental testing, focusing on added functionality in each incremet|Continuous testing throughout the development process, refining features in each iteration.
Flexibility|Easier to accommodate changes and enhancements|Adaptable to changing requirements; allows for continous refinement
Advantages|	Early delivery of partial systems; users can benefit sooner.|	Continuous refinement based on user feedback; early defect detection and correction.
Disadvantages|	Integration issues may arise; overall architecture may be affected.	|Requires thorough planning to manage multiple iterations; continuous testing may extend development time.
