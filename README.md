# Design-Patterns


![design pattern](images/dp1.png)


## Introduction

<br>

* A design patterns are well-proved solution for solving the specific problem/task.
* In software engineering, a design pattern is a general repeatable solution to a commonly occurring problem in software design. 
* A design pattern isn't a finished design that can be transformed directly into code. 
* It is a description or template for how to solve a problem that can be used in many different situations.


### Uses & Advantages

<br>

<!-- style="font-size:20px"-->
**Uses**

<br>

* Design patterns can speed up the development process by providing tested, proven development paradigms. Effective software design requires considering issues that may not become visible until later in the implementation. Reusing design patterns helps to prevent subtle issues that can cause major problems and improves code readability for coders and architects familiar with the patterns.

* Often, people only understand how to apply certain software design techniques to certain problems. These techniques are difficult to apply to a broader range of problems. Design patterns provide general solutions, documented in a format that doesn't require specifics tied to a particular problem.

* In addition, patterns allow developers to communicate using well-known, well understood names for software interactions. Common design patterns can be improved over time, making them more robust than ad-hoc designs.

<br>

<!-- style="font-size:20px"-->
**Advantage**

* They are reusable in multiple projects.
* They provide the solutions that help to define the system architecture.
* They capture the software engineering experiences.
* They provide transparency to the design of an application.
* They are well-proved and testified solutions since they have been built upon the knowledge and experience of expert software   developers.
* Design patterns dont guarantee an absolute solution to a problem. They provide clarity to the system architecture and the possibility of building a better system.

### Categorization of design patterns

<br>
Basically, design patterns are categorized into two parts:

<!-- style="font-size:20px"-->
* **Core Java (or JSE) Design Patterns.**
* **JEE Design Patterns.**


## Core Java Design Patterns

<br>

**1. Creational Design Pattern**

* Factory Pattern
* Abstract Factory Pattern
* Singleton Pattern
* Prototype Pattern
* Builder Pattern.

<br>

**2. Structural Design Pattern**


* Adapter Pattern
* Bridge Pattern
* Composite Pattern
* Decorator Pattern
* Facade Pattern
* Flyweight Pattern
* Proxy Pattern

<br>

**3. Behavioral Design Pattern**

* Chain Of Responsibility Pattern
* Command Pattern
* Interpreter Pattern
* Iterator Pattern
* Mediator Pattern
* Memento Pattern
* Observer Pattern
* State Pattern
* Strategy Pattern
* Template Pattern
* Visitor Pattern


## Creational Design Pattern

<br>

* **Creational design patterns** are concerned with the way of creating objects. 
* These design patterns are used when a decision must be made at the time of instantiation of a class (i.e. creating an object of a class).

* But everyone knows an object is created by using new keyword in java. **For example:**

<br>

```
StudentRecord s1=new StudentRecord();  
```

<br>

<!-- style="font-size:20px"-->
**Types of creational design patterns**

<!-- style="font-size:20px"-->
* Factory Pattern
* Abstract Factory Pattern
* Singleton Pattern
* Prototype Pattern
* Builder Pattern.


### Factory Method Pattern

<br>

* A **Factory Pattern** or **Factory Method Pattern** defines an interface or abstract class for creating an object but let the subclasses decide which class to instantiate. 
* In other words, subclasses are responsible to create the instance of the class.
* The Factory Method Pattern is also known as **Virtual Constructor**.

<br>

<!-- style="font-size:20px"-->
**Advantage of Factory Design Pattern**

Factory Method Pattern allows the sub-classes to choose the type of objects to create.
It promotes the loose-coupling by eliminating the need to bind application-specific classes into the code. That means the code interacts solely with the resultant interface or abstract class, so that it will work with any classes that implement that interface or that extends that abstract class.

<br>

<!-- style="font-size:20px"-->
**Usage of Factory Design Pattern**

When a class doesn't know what sub-classes will be required to create
When a class wants that its sub-classes specify the objects to be created.
When the parent classes choose the creation of objects to its sub-classes.


#### UML for Factory Method Pattern

<br>

* We are going to create a Plan abstract class and concrete classes that extends the Plan abstract class. A factory class GetPlanFactory is defined as a next step.
* GenerateBill class will use GetPlanFactory to get a Plan object. It will pass information (DOMESTICPLAN / COMMERCIALPLAN / INSTITUTIONALPLAN) to GetPalnFactory to get the type of object it needs.


![Uml](images/dp2.png)


#### A Real World Example of Factory Method

<br>

<!-- style="font-size:20px"-->
**Step 1 :** Create a Plan abstract class.

<br>

```
import java.io.*;      
abstract class Plan{  
         protected double rate;  
         abstract void getRate();  
   
         public void calculateBill(int units){  
              System.out.println(units*rate);  
          }  
} //end of Plan class. 
```

<br>

<!-- style="font-size:20px"-->
**Step 2 :** Create the concrete classes that extends Plan abstract class.

<br>

```
class  DomesticPlan extends Plan{  
        //@override  
         public void getRate(){  
             rate=3.50;              
        }  
   } //end of DomesticPlan class. 
```

```
class  CommercialPlan extends Plan{  
   //@override   
    public void getRate(){   
        rate=7.50;  
   } //end of CommercialPlan class. 
``` 

```
class  InstitutionalPlan extends Plan{  
   //@override  
    public void getRate(){   
        rate=5.50;  
   }   //end of InstitutionalPlan class. 
```

<br>

<!-- style="font-size:20px"-->
**Step 3 :** Create a GetPlanFactory to generate object of concrete classes based on given information..

<br>

```
class GetPlanFactory{  
      
   //use getPlan method to get object of type Plan   
       public Plan getPlan(String planType){  
            if(planType == null){  
             return null;  
            }  
          if(planType.equalsIgnoreCase("DOMESTICPLAN")) {  
                 return new DomesticPlan();  
               }   
           else if(planType.equalsIgnoreCase("COMMERCIALPLAN")){  
                return new CommercialPlan();  
            }   
          else if(planType.equalsIgnoreCase("INSTITUTIONALPLAN")) {  
                return new InstitutionalPlan();  
          }  
      return null;  
   }  
}//end of GetPlanFactory class.  

```

<br>

<!-- style="font-size:20px"-->
**Step 4 :** Generate Bill by using the GetPlanFactory to get the object of concrete classes by passing an information such as type of plan DOMESTICPLAN or COMMERCIALPLAN or INSTITUTIONALPLAN.

<br>

```
import java.io.*;    
class GenerateBill{  
    public static void main(String args[])throws IOException{  
      GetPlanFactory planFactory = new GetPlanFactory();  
        
      System.out.print("Enter the name of plan for which the bill will be generated: ");  
      BufferedReader br=new BufferedReader(new InputStreamReader(System.in));  
  
      String planName=br.readLine();  
      System.out.print("Enter the number of units for bill will be calculated: ");  
      int units=Integer.parseInt(br.readLine());  
  
      Plan p = planFactory.getPlan(planName);  
      //call getRate() method and calculateBill()method of DomesticPaln.  
  
       System.out.print("Bill amount for "+planName+" of  "+units+" units is: ");  
           p.getRate();  
           p.calculateBill(units);  
            }  
    }//end of GenerateBill class.
```  

<!-- style="font-size:20px;color:red"-->
**OUTPUT :**

![output](images/dp3.png)


#### Abstract Factory Pattern

<br>

* Abstract Factory Pattern defines an interface or abstract class for creating families of related (or dependent) objects but without specifying their concrete sub-classes.
* That means Abstract Factory lets a class returns a factory of classes. So, this is the reason that Abstract Factory Pattern is one level higher than the Factory Pattern.

* An Abstract Factory Pattern is also known as **Kit**.
