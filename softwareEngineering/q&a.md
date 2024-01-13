# Question & Answers

# Table of Content
- [Question \& Answers](#question--answers)
- [Table of Content](#table-of-content)
- [What is ADUP?](#what-is-adup)
  - [Why ADUP is better than 'all paths' testing?](#why-adup-is-better-than-all-paths-testing)
- [What is a 'CRUD' check?](#what-is-a-crud-check)
  - [CRUD Operations Breakdown](#crud-operations-breakdown)
- [What is Temporal Logic](#what-is-temporal-logic)
  - [Branches](#branches)

# What is ADUP?
ADUP stands for "All-DU Paths," which is a testing technique used in software testing and code coverage analysis. It is a coverage criterion that focuses on ensuring the coverage of all "DU" (Define-Use) paths within a program.

In programming, a "Define-Use" path refers to the sequence of operations involving the definition and subsequent use of variables or data within the code. The ADUP criterion aims to test all possible paths in the program where a variable or data is defined and then used.

The ADUP testing technique ensures that all combinations of paths where a variable's value is defined and subsequently used are covered during testing. This helps in identifying potential issues related to variable initialization, assignment, and usage, aiming to increase the thoroughness of testing by considering these specific paths.

By covering all Define-Use paths, ADUP testing aims to enhance code coverage and ensure that variables are appropriately utilized throughout the execution of the software, thereby potentially reducing the likelihood of undetected errors or issues related to variable handling in the code.

## Why ADUP is better than 'all paths' testing?
The All Define Use Paths (ADUP) testing is better than all paths testing **because it focuses on identifying and testing the specific paths within a software system that are defined by the use of variables or data**.
- ADUP testing narrows down the test coverage to those paths explicitly affected by the usage of variables, thereby potentially reducing the testing effort while ensuring thorough coverage of critical pathways that could impact the system's behavior or outcomes. 
- This targeted approach enhances efficiency by concentrating on relevant paths influenced by variable usage, offering a more focused and effective testing strategy compared to attempting to cover all possible paths, including those not influenced by variable usage in the software system.

# What is a 'CRUD' check?
In software engineering, a CRUD refers to a validation process that ensures proper functionality and compliance with the CRUD (Create, Read, Update, Delete) operations within the system.

What are CRUD Operations? CRUD operations are fundamental functions used in database and application development to mange data.

A CRUD check is a validation process performed during software development or testing to ensure that the application or system functions correctly and securely while performing these CRUD operations.

**A CRUD check is a cross model check between the functional and data models.**

## CRUD Operations Breakdown
|Operation|Breakdown Details|Test to verify
|-|-|-|
Create|The operation involves adding new data or records to a system or database.|Ensuring that new data can be successfully added to the system without errors or incosistencies. This includes validating input formats, constraints, and data integrity.
Read|It involves retrieving or reading existing data or records from a system or database.|Confirming that the system can retrieve and display existing data accurantely without errors or data corruption. This includes checking for proper access permissions and data filtering.
Update|This operation allows modifying or updating existing data or records within a system.|Validating that the system allows modifying existing data ccorrectly, ensuring that changes are accurately reflected in the system and do not cause unexpected behaviour or data loss.
Delete|It involves removing or deleting data ir records from a system or database.|Ensuring that the system can remove data or records safely without affecting the integrity of the system of causing data loss. This inlcudes checking for casacading deletions and proper handling of related data.

# What is Temporal Logic
Temporal Logic is a formal system used in computer science, mathematics, and philosophy to reason about and express properties of concurrent and reactive systems. Temporal logic helps in describing and reasoning about temporal aspects such as the ordering of events within a system.

## Branches
There are two main branches of temporal logic used:
|Branch|Description|Example|
|-|-|-|