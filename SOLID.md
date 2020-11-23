# SOLID Programming

## Abstract

At times, when we are delving into new projects, we may often face the prospect of being accountable for the clumsy code we write. It is in no one's intention to write poot code, but without proper control and practice, we may get subjected to the chaos and end up with an ineptly written code. This is where the **SOLID Design Principles** come into action. In this paper, I will be briefly going through the SOLID design concept with a few code samples.

## Introduction to SOLID

 The SOLID principle is a type of coding procedure for Object-Oriented Design intended to make the code reusable, readable, flexible, and maintainable. It was introduced by Robert C. Martin in his 2000 paper, [*"Design Principles and Design Patterns"*](https://web.archive.org/web/20150906155800/http:/www.objectmentor.com/resources/articles/Principles_and_Patterns.pdf), and the term was coined by Micheal Feathers. SOLID is an acronym which stands for:
   1) **S**ingle Responsibility Principle
   2) **O**pen and Closed Principle
   3) **L**iskov Substitution Principle
   4) **I**nterface Segregation Principle
   5) **D**ependancy Inversion Principle

## Why SOLID? - The rotting design
While writing a code, there are many small flaws we oversee, and these accumulate to rot our program and over time, any efforts at simple changes can prove much tiring and unfruitful. We can identify whether our system is rotting by analyzing its rigidity, fragility, mobility, and viscosity.

## Design Concepts

### 1. Single Responsibility Principle
  *A class should have a single responsibility and a single reason to change*

#### Example