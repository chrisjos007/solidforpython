# SOLID Programming

## Abstract

At times, when we are delving into new projects, we may often face the prospect of being accountable for the clumsy code we write. It is in no one's intention to write poor code, but without proper control and practice, we may get subjected to the chaos and end up with an ineptly written code. This is where the **SOLID Design Principles** come into action. In this paper, I will be briefly going through the SOLID design concept with a few code samples.

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

### **1. Single Responsibility Principle (SRP)**
  *A class should have a single responsibility and a single reason to change*

When we are required to add functionality to a program, it is wrong to append everything into existing classes. Rather, each functionality needs to be wrapped up into separate classes whose functionality should be the sole reason for any modifications in the class. Excessive coupling needs to be avoided as it makes introducing changes difficult.
##### SRP fail
      class student:
          def __init__(self, name):
            self.name = name
          
          def savepersonalinfo(self, info):
            # students personal info

          def savescore(self, scores):
            # student scores
The above example is a clear violation of the SRP principle as the student class is having the responsibility of storing the student's personal information as well as academic information. So any attempts at modification in the academic database can have adverse effects on the personal information and any classes that use it. A simple solution to this is splitting up each task into separate classes.

Now a downside to this is the requirement of a large number of interdependent classes that can be quite messy. It can be resolved by executing the *Facade pattern* that corresponds to wrapping up similar items to hide the implementation details.


### **2.Open-Closed Principle (OCP)**
*Software entities should be open for extension, but closed for modification*

A program that follows the open-close principle can have additional features applied to it by extending the existing classes rather than modifying them. Now consider the example below:

##### OCP fail
      class academic:
          def __init__ (self, student, score):
              self.student = student
              self.scores = scores
          
          def scorenorm(self, difficulty):
              if difficulty == 'normal':
                  return self.scores+3
              elif difficulty == 'hard':
                  return self.scores+6
Now for the above problem, assume that the teacher has decided to give additional marks for "very hard" difficulty. Then we have to add additional else cases that modify the base class which is a clear violation of OCP. So by applying OCP, we can rewrite the base class.

##### refactored
        class academic:
            def __init__ (self, student, score):
                ​self.student = student
                ​self.scores = scores

            def scorenorm(self):
                return self.scores+3

        class normhard(academic):
          """normalizes for hard difficulty"""
            def scorenorm(self):
                return super().scorenorm()+3

        class normextreme(normhard):
          """normalizes for extreme difficluty"""
            def scorenorm(self):
                return super().scorenorm()+3


### **3.Liskov Substitution Principle (LSP)**
*If S is a subtype of T, then objects of T may be replaced with objects of type S without affecting the logic of the program*

The credit for this principle goes to Barbar Liskov. Simply put, a subclass must be substitutable in place of its superclass without affecting the correctness of the program. Now, this may come off as being confusing to grasp, but we can analyze the example below and try to understand it.

##### LSP fail
        class academics:
            def __init__ (self, name, details):
                self.name = name
                self.address = details

            def scores(self):
                # student scores

            def normscores(self):
                # normalize student scores


        class science(academics):
            def normscores(self):
                pass


        class commerce(academics):
            def normscores(self):
                pass
Consider the case when the science exam marks are normalized and commerce marks are not. Then this code violates LSP as the commerce class cannot be substituted in place of its parent class. Hence this code requires refactoring as we can see below:

##### refactored
        class academics:
            """ student's academic details """
            def __init__ (self, name, details):
                """ store details """
                self.name = name
                self.address = details

            def savescores(self):
                # student scores


        class needsnorm(academics):
            """ calculates normalized scores """
            def normscores(self):
                # normalize student scores

            def getscores(self):
                # returns scores


        class nonorms(academics):
            def getscores(self):
                # returns scores


        class science(needsnorm):
            """A subject that requires normalization"""
            def getscores(self):
                pass


        class commerce(nonorms):
            """A Subject not requiring normalization"""
            def getscores(self):               
                pass
In this case, the child classes are interchangeable with the parent class. The LSP is essential to Object-Oriented Design as it emphasizes polymorphism. Child classes derived from a parent should have attributes that can replace the parent class that has been implemented here.

### **4.Interface Segregation Principle (ISP)**
*No clients should be forced to depend upon interfaces that they do not use*

Make client-specific interfaces that should do their specific jobs. Simple light interfaces are preferable over "fat" interfaces. This can be seen as an extension of the Single Responsibility Principle. Consider the example of an interface that finds the normalized scores of subjects.

##### ISP fail

        class norm:
            def engnorm(self):
              """normalize english scores"""

            def mathnorm(self)
              """ normalize maths scores """

            def sciencenorm(self):
              """normalize science scores"""

Now each subject class that calculates the normalized scores will be having methods for the other subjects and as we add more subjects, everything will end up crashing down. So we move on to solving this dilemma using the ISP concept by segregating our actions to separate interfaces as shown below.

##### refactored
        class  norm:
            def normalize(self):
                """normalize scores"""


        class english(norm):
            def normalize(self):
                pass


        class science(norm):
            def normalize(self):
                pass


        class math(norm):
            def normalize(self):
                pass

Even though python does not have interfaces, it is of importance to python developers as it can be used to add simple functionalities that can be implemented easily as opposed to the large unnecessary functionalities of fat interfaces.


### **5.Dependancy Inversion Principle (DIP)**

*High-level modules should not depend on low-level modules. Both should depend on abstractions.
Abstractions should not depend on details, rather details should depend on abstractions.*

We can see that all the principles leading up to this one are wrapping up on the concept of non-dependency on detail. It is an essential concept in the implementation of reusable frameworks. This principle is an implementation of decoupling as tightly coupling high-level modules or classes to low-level modules or classes can cause a serious pushback if any alterations are required in the low-level modules that are typically undesirable.

## Conclusion

SOLID defines the way a system needs to be designed. Refactoring is not intended to make the code simpler or short, it is implemented to ensure scalability, flexibility, extensibility, and maintainability. A developer working on a refactored code can easily add functionalities that adhere to the normal functioning of the code without driving everything into chaos. It is important to note that writing good code is always based on the simple notion of the **DRY principle**. Following the SOLID and DRY principle does not make one a perfect programmer, but it can help them reach two steps closer to that goal.