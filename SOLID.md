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
While writing a code, there are many small flaws that we oversee, and these accumulate to rot our program and over time, any efforts at simple changes can prove much tiring and unfruitful. We can identify whether our system is rotting by analyzing its rigidity, fragility, mobility, and viscosity.

## Design Concepts

### 1. Single Responsibility Principle
  *A class should have a single responsibility and a single reason to change*

When we are required to add functionality to a program, it is wrong to append everything into existing classes. Rather, each functionalty needs to be wrapped up into separate classes whose functionality should be the sole reason for any modifications in the class.
#### Example
      class student:
          def __init__(self, name):
            self.name = name
          
          def savepersonalinfo(self, info):
            # students personal info

          def savescore(self, scores):
            # student scores
The above example is a clear violation of the SRP principle as the student class is having the responsibility of storing the student's personal information as well as academic information. So any attempts at modification in the academic database can have adverse effects on the personal information and any classes that use it. Now a downside to this is the requirement of a large number of interdependent classes which can be resolved by executing the *Facade pattern* which corresponds to wrapping up similar items to hide the implementation details.

### 2.Open-Closed Principle
*Software entities should be open for extension, but closed for modification*

Now consider the example below:

      class academic:
          def __init__ (self, student, score):
              self.student = student
              self.scores = scores
          
          def scorenorm(self, difficulty):
              if difficulty == 'normal':
                  return self.scores+3
              elif difficulty == 'hard':
                  return self.scores+6
