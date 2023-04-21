# Design-Patterns


![design pattern](images/dp1.png)


# Introduction

<br>

* A design patterns are well-proved solution for solving the specific problem/task.
* In software engineering, a design pattern is a general repeatable solution to a commonly occurring problem in software design. 
* A design pattern isn't a finished design that can be transformed directly into code. 
* It is a description or template for how to solve a problem that can be used in many different situations.


## Uses & Advantages

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

## Categorization of design patterns

<br>
Basically, design patterns are categorized into two parts:

<!-- style="font-size:20px"-->
* **Core Java (or JSE) Design Patterns.**
* **JEE Design Patterns.**


# Core Java Design Patterns

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


# Creational Design Pattern

<br>

* **Creational design patterns** are concerned with the way of creating objects. 
* These design patterns are used when a decision must be made at the time of instantiation of a class (i.e. creating an object of a class).

* But everyone knows an object is created by using new keyword in java. **For example:**

<br>

```java
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


## Factory Method Pattern

<br>

* A **Factory Pattern** or **Factory Method Pattern** defines an interface or abstract class for creating an object but let the subclasses decide which class to instantiate. 
* In other words, subclasses are responsible to create the instance of the class.
* The Factory Method Pattern is also known as **Virtual Constructor**.

<br>

<!-- style="font-size:20px"-->
**Advantage of Factory Design Pattern**

* Factory Method Pattern allows the sub-classes to choose the type of objects to create.
* It promotes the loose-coupling by eliminating the need to bind application-specific classes into the code. That means the code interacts solely with the resultant interface or abstract class, so that it will work with any classes that implement that interface or that extends that abstract class.

<br>

<!-- style="font-size:20px"-->
**Usage of Factory Design Pattern**

* When a class doesn't know what sub-classes will be required to create
* When a class wants that its sub-classes specify the objects to be created.
* When the parent classes choose the creation of objects to its sub-classes.


### UML for Factory Method Pattern

<br>

* We are going to create a Plan abstract class and concrete classes that extends the Plan abstract class. A factory class GetPlanFactory is defined as a next step.
* GenerateBill class will use GetPlanFactory to get a Plan object. It will pass information (DOMESTICPLAN / COMMERCIALPLAN / INSTITUTIONALPLAN) to GetPalnFactory to get the type of object it needs.


![Uml](images/dp2.png)


### A Real World Example of Factory Method

<br>

<!-- style="font-size:20px;"--> 
* [Create a Plan abstract class](#create-a-plan-abstract-class)
* [Create the concrete classes](#create-the-concrete-classes-that-extends-plan-abstract-class)
* [Create a GetPlanFactory ](#create-a-getplanfactory-to-generate-object-of-concrete-classes)
* [Generate Bill by using the GetPlanFactory ](#generate-bill-by-using-the-getplanfactory)


#### Create a Plan abstract class

<br>

```java
import java.io.*;      
abstract class Plan{  
         protected double rate;  
         abstract void getRate();  
   
         public void calculateBill(int units){  
              System.out.println(units*rate);  
          }  
} //end of Plan class. 
```



#### Create the concrete classes that extends Plan abstract class

<br>

```java
class  DomesticPlan extends Plan{  
        //@override  
         public void getRate(){  
             rate=3.50;              
        }  
   } //end of DomesticPlan class. 
```

```java
class  CommercialPlan extends Plan{  
   //@override   
    public void getRate(){   
        rate=7.50;  
   } //end of CommercialPlan class. 
``` 

```java
class  InstitutionalPlan extends Plan{  
   //@override  
    public void getRate(){   
        rate=5.50;  
   }   //end of InstitutionalPlan class. 
```



#### Create a GetPlanFactory to generate object of concrete classes

<br>

```java
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

#### Generate Bill by using the GetPlanFactory 

<br>

* Generate Bill by using the GetPlanFactory to get the object of concrete classes by passing an information such as type of plan DOMESTICPLAN or COMMERCIALPLAN or INSTITUTIONALPLAN.

```java
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
#### OUTPUT 

![output](images/dp3.png)


## Abstract Factory Pattern

<br>

* Abstract Factory Pattern defines an interface or abstract class for creating families of related (or dependent) objects but without specifying their concrete sub-classes.
* That means Abstract Factory lets a class returns a factory of classes. So, this is the reason that Abstract Factory Pattern is one level higher than the Factory Pattern.

* An Abstract Factory Pattern is also known as **Kit**.

<br>

<!-- style="font-size:20px"-->
**Advantage of Abstract Factory Pattern**

* Abstract Factory Pattern isolates the client code from concrete (implementation) classes.
* It eases the exchanging of object families.
* It promotes consistency among objects.

<br>

<!-- style="font-size:20px"-->
**Usage of Abstract Factory Pattern**

* When the system needs to be independent of how its object are created, composed, and represented.
* When the family of related objects has to be used together, then this constraint needs to be enforced.
* When you want to provide a library of objects that does not show implementations and only reveals interfaces.
* When the system needs to be configured with one of a multiple family of objects.


### UML for Abstract Factory Pattern

<br>

* We are going to create a Bank interface and a Loan abstract class as well as their sub-classes.
* Then we will create AbstractFactory class as next step.
* Then after we will create concrete classes, BankFactory, and LoanFactory that will extends AbstractFactory class
* After that, AbstractFactoryPatternExample class uses the FactoryCreator to get an object of AbstractFactory class.

<br>

![Abstarct pattern UML](images/dp4.png)


### Example of Abstract Factory Pattern

<br>

* Here, we are calculating the loan payment for different banks like **HDFC, ICICI, SBI** etc.

<br>

<!-- style="font-size:20px;"--> 
1. [Create a Bank interface](#create-a-bank-interface)
2. [Create concrete classes](#create-concrete-classes)
3. [Create the Loan abstract class](#create-the-loan-abstract-class)
4. [Create concrete classes that extend the Loan abstract class](#create-concrete-classes-that-extend-the-loan-abstract-class)
5. [Create an abstract class](#create-an-abstract-class)
6. [Create the factory classes that inherit AbstractFactory class](#create-the-factory-classes-that-inherit-abstractfactory-class)
7. [Create a FactoryCreator class](#create-a-factorycreator-class)
8. [Use the FactoryCreator to get AbstractFactory](#use-the-factorycreator-to-get-abstractfactory)


#### Create a Bank interface

<br>

```java
import java.io.*;     
interface Bank{  
        String getBankName();  
}  
```



#### Create concrete classes

<br>

```java
class HDFC implements Bank{  
         private final String BNAME;  
         public HDFC(){  
                BNAME="HDFC BANK";  
        }  
        public String getBankName() {  
                  return BNAME;  
        }  
}  
```

```java
class ICICI implements Bank{  
       private final String BNAME;  
       ICICI(){  
                BNAME="ICICI BANK";  
        }  
        public String getBankName() {  
                  return BNAME;  
       }  
}  
```

```java
class SBI implements Bank{  
      private final String BNAME;  
      public SBI(){  
                BNAME="SBI BANK";  
        }  
       public String getBankName(){  
                  return BNAME;  
       }  
}
```  



#### Create the Loan abstract class

<br>

```java
abstract class Loan{  
   protected double rate;  
   abstract void getInterestRate(double rate);  
   public void calculateLoanPayment(double loanamount, int years)  
   {  
        /* 
              to calculate the monthly loan payment i.e. EMI   
                            
              rate=annual interest rate/12*100; 
              n=number of monthly installments;            
              1year=12 months. 
              so, n=years*12; 
 
            */  
                
         double EMI;  
         int n;  
  
         n=years*12;  
         rate=rate/1200;  
         EMI=((rate*Math.pow((1+rate),n))/((Math.pow((1+rate),n))-1))*loanamount;  
  
System.out.println("your monthly EMI is "+ EMI +" for the amount"+loanamount+"
 you have borrowed");     
 }  
}// end of the Loan abstract class. 
``` 


#### Create concrete classes that extend the Loan abstract class

<br>

```java
class HomeLoan extends Loan{  
     public void getInterestRate(double r){  
         rate=r;  
    }  
}//End of the HomeLoan class.  
```

```java
class BussinessLoan extends Loan{  
    public void getInterestRate(double r){  
          rate=r;  
     }  
  
}//End of the BusssinessLoan class.  
```

```java
class EducationLoan extends Loan{  
     public void getInterestRate(double r){  
       rate=r;  
 }  
}//End of the EducationLoan class. 
```



#### Create an abstract class

<br>

* Create an abstract class (i.e AbstractFactory) to get the factories for Bank and Loan Objects.

```java
abstract class AbstractFactory{  
  public abstract Bank getBank(String bank);  
  public abstract Loan getLoan(String loan);  
}
```  


#### Create the factory classes that inherit AbstractFactory class 

<br>

* Create the factory classes that inherit AbstractFactory class to generate the object of concrete class based on given information.

```java
class BankFactory extends AbstractFactory{  
   public Bank getBank(String bank){  
      if(bank == null){  
         return null;  
      }  
      if(bank.equalsIgnoreCase("HDFC")){  
         return new HDFC();  
      } else if(bank.equalsIgnoreCase("ICICI")){  
         return new ICICI();  
      } else if(bank.equalsIgnoreCase("SBI")){  
         return new SBI();  
      }  
      return null;  
   }  
  public Loan getLoan(String loan) {  
      return null;  
   }  

}//End of the BankFactory class.
```

```java
class LoanFactory extends AbstractFactory{  
           public Bank getBank(String bank){  
                return null;  
          }  
        
     public Loan getLoan(String loan){  
      if(loan == null){  
         return null;  
      }  
      if(loan.equalsIgnoreCase("Home")){  
         return new HomeLoan();  
      } else if(loan.equalsIgnoreCase("Business")){  
         return new BussinessLoan();  
      } else if(loan.equalsIgnoreCase("Education")){  
         return new EducationLoan();  
      }  
      return null;  
   }  
     
}  
```

#### Create a FactoryCreator class

<br>

* Create a FactoryCreator class to get the factories by passing an information such as Bank or Loan.

```java
class FactoryCreator {  
     public static AbstractFactory getFactory(String choice){  
      if(choice.equalsIgnoreCase("Bank")){  
         return new BankFactory();  
      } else if(choice.equalsIgnoreCase("Loan")){  
         return new LoanFactory();  
      }  
      return null;  
   }  
}//End of the FactoryCreator. 
``` 



#### Use the FactoryCreator to get AbstractFactory

<br>

* Use the FactoryCreator to get AbstractFactory*  in order to get factories of concrete classes by passing an information such as type.

```java
import java.io.*;  
class AbstractFactoryPatternExample {  
      public static void main(String args[])throws IOException {  
       
      BufferedReader br=new BufferedReader(new InputStreamReader(System.in));  
  
      System.out.print("Enter the name of Bank from where you want to take loan amount: ");  
      String bankName=br.readLine();  
  
System.out.print("\n");  
System.out.print("Enter the type of loan e.g. home loan or business loan or education 
loan : ");  
  
String loanName=br.readLine();  
AbstractFactory bankFactory = FactoryCreator.getFactory("Bank");  
Bank b=bankFactory.getBank(bankName);  
  
System.out.print("\n");  
System.out.print("Enter the interest rate for "+b.getBankName()+ ": ");  
  
double rate=Double.parseDouble(br.readLine());  
System.out.print("\n");  
System.out.print("Enter the loan amount you want to take: ");  
  
double loanAmount=Double.parseDouble(br.readLine());  
System.out.print("\n");  
System.out.print("Enter the number of years to pay your entire loan amount: ");  
int years=Integer.parseInt(br.readLine());  
  
System.out.print("\n");  
System.out.println("you are taking the loan from "+ b.getBankName());  
  
AbstractFactory loanFactory = FactoryCreator.getFactory("Loan");  
           Loan l=loanFactory.getLoan(loanName);  
           l.getInterestRate(rate);  
           l.calculateLoanPayment(loanAmount,years);  
  }  
}//End of the  AbstractFactoryPatternExample   
```

<br>

<!-- style="font-size:20px;color:red"-->
#### OUTPUT

<br>

![output](images/dp5.png)


## Singleton design pattern in Java

<br>

* Singleton Pattern says that just"define a class that has only one instance and provides a global point of access to it".

* In other words, a class must ensure that only single instance should be created and single object can be used by all other classes.

<br>

<!-- style="font-size:20px;"-->
There are two forms of singleton design pattern

* **Early Instantiation :** creation of instance at load time.
* **Lazy Instantiation :** creation of instance when required.

<br>

<!-- style="font-size:20px;"-->
Advantage of Singleton design pattern

* Saves memory because object is not created at each request. Only single instance is reused again and again.



<br>

<!-- style="font-size:20px;"-->
Usage of Singleton design pattern

* Singleton pattern is mostly used in multi-threaded and database applications. 
* It is used in logging, caching, thread pools, configuration settings etc.

### Uml of Singleton design pattern

![singleton design pattern](images/dp6.png)


### Creating Singleton design pattern

<br>

To create the singleton class, we need to have static member of class, private constructor and static factory method.


* **Static member :** It gets memory only once because of static, itcontains the instance of the Singleton class.
* **Private constructor :** It will prevent to instantiate the Singleton class from outside the class.
* **Static factory method :** This provides the global point of access to the Singleton object and returns the instance to the caller.


### Early Instantiation of Singleton Pattern

<br>

In such case, we create the instance of the class at the time of declaring the static data member, so instance of the class is created at the time of classloading.

Let's see the example of singleton design pattern using early instantiation.

<br>


```java
class A{  
 private static A obj=new A();//Early, instance will be created at load time  
 private A(){}  
   
 public static A getA(){  
  return obj;  
 }  
  
 public void doSomething(){  
 //write your code  
 }  
}
```

### Lazy Instantiation of Singleton Pattern

<br>

In such case, we create the instance of the class in synchronized method or synchronized block, so instance of the class is created when required.

Let's see the simple example of singleton design pattern using lazy instantiation.

```java
class A{  
 private static A obj;  
 private A(){}  
   
 public static A getA(){  
   if (obj == null){  
      synchronized(Singleton.class){  
        if (obj == null){  
            obj = new Singleton();//instance will be created at request time  
        }  
    }              
    }  
  return obj;  
 } 

  
 public void doSomething(){  
 //write your code  
 }  
}  
```

### Significance of Serialization in Singleton Pattern

<br>

* If singleton class is Serializable, you can serialize the singleton instance. Once it is serialized, you can deserialize it but it will not return the singleton object.

* To resolve this issue, you need to override the readResolve() method that enforces the singleton. It is called just after the object is deserialized. It returns the singleton object.

<br>

```java
public class A implements Serializable {  
        //your code of singleton  
        protected Object readResolve() {  
            return getA();  
        }  
  
    } 
```

#### Real Example of Singleton Pattern

<br>

* We are going to create a JDBCSingleton class. This JDBCSingleton class contains its constructor as private and a private static instance jdbc of itself.
* JDBCSingleton class provides a static method to get its static instance to the outside world. Now, JDBCSingletonDemo class will use JDBCSingleton class to get the JDBCSingleton object.

![example](images/dp7.png)


<!-- style="font-size:20px;"-->
click on the below link for the complete code example:

https://github.com/dharmananda4444/Design-Patterns/tree/version-1.0/code/singleton


#### Outputs

![output1](images/dp8.png)

![output2](images/dp9.png)

![output3](images/dp10.png)


## Prototype Design Pattern

<br>

Prototype Pattern says that cloning of an existing object instead of creating new one and can also be customized as per the requirement.

This pattern should be followed, if the cost of creating a new object is expensive and resource intensive.

<br>

<!-- style="font-size:20px;"-->
**Advantage of Prototype Pattern**

* It reduces the need of sub-classing.
* It hides complexities of creating objects.
* The clients can get new objects without knowing which type of object it will be.
* It lets you add or remove objects at runtime.

<br>

<!-- style="font-size:20px;"-->
**Usage of Prototype Pattern**

* When the classes are instantiated at runtime.
* When the cost of creating an object is expensive or complicated.
* When you want to keep the number of classes in an application minimum.
* When the client application needs to be unaware of object creation and representation.

### UML for Prototype Pattern

![Uml](images/dp11.png)

* We are going to create an interface Prototype that contains a method getClone() of Prototype type.
* Then, we create a concrete class EmployeeRecord which implements Prototype interface that does the cloning of EmployeeRecord object.
* PrototypeDemo class will uses this concrete class EmployeeRecord.


### Example of Prototype Design Pattern

<br>

**Prototype.java**

```java
interface Prototype {  
  
     public Prototype getClone();  
      
}//End of Prototype interface.
```

<br>

**File: EmployeeRecord.java**

```java
class EmployeeRecord implements Prototype{  
      
   private int id;  
   private String name, designation;  
   private double salary;  
   private String address;  
      
   public EmployeeRecord(){  
            System.out.println("   Employee Records of Oracle Corporation ");  
            System.out.println("---------------------------------------------");  
            System.out.println("Eid"+"\t"+"Ename"+"\t"+"Edesignation"+"\t"+"Esalary"+
            "\t\t"+"Eaddress");  
      
}  

  
 public  EmployeeRecord(int id, String name, String designation, double salary, 
 String address) {  
          
        this();  
        this.id = id;  
        this.name = name;  
        this.designation = designation;  
        this.salary = salary;  
        this.address = address;  
    }  
 
      
  public void showRecord(){  
          
        System.out.println(id+"\t"+name+"\t"+designation+"\t"+salary+"\t"+address);  
   }  
  
    @Override  
    public Prototype getClone() {  
          
        return new EmployeeRecord(id,name,designation,salary,address);  
    }  
}//End of EmployeeRecord class.
```  

<br>

**File: PrototypeDemo.java**

```java
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStreamReader;  
  
class PrototypeDemo{  
     public static void main(String[] args) throws IOException {  
          
        BufferedReader br =new BufferedReader(new InputStreamReader(System.in));  
        System.out.print("Enter Employee Id: ");  
        int eid=Integer.parseInt(br.readLine());  
        System.out.print("\n");  
          
        System.out.print("Enter Employee Name: ");  
        String ename=br.readLine();  
        System.out.print("\n");  
          
        System.out.print("Enter Employee Designation: ");  
        String edesignation=br.readLine();  
        System.out.print("\n");  
          
        System.out.print("Enter Employee Address: ");  
        String eaddress=br.readLine();  
        System.out.print("\n");  
          
        System.out.print("Enter Employee Salary: ");  
        double esalary= Double.parseDouble(br.readLine());  
        System.out.print("\n");  
           
        EmployeeRecord e1=new EmployeeRecord(eid,ename,edesignation,esalary,eaddress);  
          
        e1.showRecord();  
        System.out.println("\n");  
        EmployeeRecord e2=(EmployeeRecord) e1.getClone();  
        e2.showRecord();  
    }     
}//End of the ProtoypeDemo class. 
```

### Output

![output](images/dp12.png)


## Builder Design Pattern

<br>

Builder Pattern says that "construct a complex object from simple objects using step-by-step approach"

It is mostly used when object can't be created in single step like in the de-serialization of a complex object.

<br>

<!-- style="font-size:20px;"--> 
**Advantage of Builder Design Pattern**

* It provides clear separation between the construction and representation of an object.
* It provides better control over construction process.
* It supports to change the internal representation of objects.


### UML for Builder Pattern Example

<br>

![Uml](images/dp13.png)


### Example of Builder Design Pattern

<br>

To create simple example of builder design pattern, you need to follow **6** following steps :

<!-- style="font-size:20px;"--> 
* [Create Packing interface](#create-packing-interface)
* [Create 2 abstract classes CD and Company](#create-2-abstract-classes-cd-and-company)
* [Create 2 implementation classes of Company: Sony and Samsung](#create-2-implementation-classes-of-company-sony-and-samsung)
* [Create the CDType class](#create-the-cdtype-class)
* [Create the CDBuilder class](#create-the-cdbuilder-class)
* [Create the BuilderDemo class](#create-the-builderdemo-class)


#### Create Packing interface

<br>

**File: Packing.java**


```java
public interface Packing {  
            public String pack();  
            public int price();  
} 
``` 

#### Create 2 abstract classes CD and Company

<br>

* Create an abstract class CD which will implement Packing interface.

<br>

**File: CD.java**

```java
public abstract class CD implements Packing{  
public abstract String pack();  
}  
```

**File: Company.java**

```java
public abstract class Company extends CD{  
   public abstract int price();  
}  
```

#### Create 2 implementation classes of Company Sony and Samsung

<br>

**File: Sony.java**

```java
public class Sony extends Company{  
    @Override  
        public int price(){   
                        return 20;  
      }  
    @Override  
    public String pack(){  
             return "Sony CD";  
        }         
}//End of the Sony class. 
``` 

<br>

**File: Samsung.java**

```java
public class Samsung extends Company {  
    @Override  
        public int price(){   
                        return 15;  
    }  
    @Override  
    public String pack(){  
             return "Samsung CD";  
        }         
}//End of the Samsung class.
```  

#### Create the CDType class

<br>

**File: CDType.java**

```java
import java.util.ArrayList;  
import java.util.List;  
public class CDType {  
             private List<Packing> items=new ArrayList<Packing>();  
             public void addItem(Packing packs) {    
                    items.add(packs);  
             }  
             public void getCost(){  
              for (Packing packs : items) {  
                        packs.price();  
              }   
             }  
             public void showItems(){  
              for (Packing packing : items){  
             System.out.print("CD name : "+packing.pack());  
             System.out.println(", Price : "+packing.price());  
          }       
            }     
}//End of the CDType class.  
```

#### Create the CDBuilder class

<br>

**File: CDBuilder.java**

```java
public class CDBuilder {  
                  public CDType buildSonyCD(){   
                     CDType cds=new CDType();  
                     cds.addItem(new Sony());  
                     return cds;  
              }  
              public CDType buildSamsungCD(){  
             CDType cds=new CDType();  
             cds.addItem(new Samsung());  
             return cds;  
              }  
}// End of the CDBuilder class.
```  

#### Create the BuilderDemo class

<br>

**File: BuilderDemo.java**

```java
public class BuilderDemo{  
 public static void main(String args[]){  
   CDBuilder cdBuilder=new CDBuilder();  
   CDType cdType1=cdBuilder.buildSonyCD();  
   cdType1.showItems();  
  
   CDType cdType2=cdBuilder.buildSamsungCD();  
   cdType2.showItems();  
 }  
}  
```

#### Output

<br>

```go
CD name : Sony CD, Price : 20  
CD name : Samsung CD, Price : 15 
``` 

## Object Pool Pattern

<br>

* Performance is the key issue during the software development and the object creation, which may be a costly step.

* Object Pool Pattern says that " **to reuse the object that are expensive to create**".

* Basically, an Object pool is a container which contains a specified amount of objects. When an object is taken from the pool, it is not available in the pool until it is put back. Objects in the pool have a lifecycle: creation, validation and destroy.

* A pool helps to manage available resources in a better way. There are many using examples: especially in application servers there are data source pools, thread pools etc.

### Advantages and Usage

<br>

<!-- style="font-size:20px;"-->
Advantage of Object Pool design pattern

* It boosts the performance of the application significantly.
* It is most effective in a situation where the rate of initializing a class instance is high.
* It manages the connections and provides a way to reuse and share them.
* It can also provide the limit for the maximum number of objects that can be created.

<br>

<!-- style="font-size:20px;"-->
Usage

* When an application requires objects which are expensive to create. Eg: there is a need of opening too many connections for the database then it takes too longer to create a new one and the database server will be overloaded.
* When there are several clients who need the same resource at different times.

### UML for Object Pool Pattern

<br>

![Uml](images/dp14.png)

### Example of Object Pool Pattern

<br>

<!-- style="font-size:20px;"-->
[1. Create an ObjectPool class that is used to create the number of objects.](#create-an-objectpool-class-that-is-used-to-create-the-number-of-objects)

<!-- style="font-size:20px;"-->
[2. Create an ExportingProcess class that will be used by ExportingTask class.](#create-an-exportingprocess-class-that-will-be-used-by-exportingtask-class)

<!-- style="font-size:20px;"-->
[3. Create an ExportingTask class that will use ExportingProcess and ObjectPool class.](#create-an-exportingtask-class-that-will-use-exportingprocess-and-objectpool-class)

<!-- style="font-size:20px;"-->
[4. Create an ObjectPoolDemo class.](#create-an-objectpooldemo-class)

#### Create an ObjectPool class

<br>

* Create an ObjectPool class that is used to create the number of objects.

**File: ObjectPool.java**

```java
import java.util.concurrent.ConcurrentLinkedQueue;  
import java.util.concurrent.Executors;  
import java.util.concurrent.ScheduledExecutorService;  
import java.util.concurrent.TimeUnit;  
  
public abstract class ObjectPool<T> {  
/* 
  pool implementation is based on ConcurrentLinkedQueue from the java.util.concurrent package. 
  ConcurrentLinkedQueue is a thread-safe queue based on linked nodes.  
   Because the queue follows FIFO technique (first-in-first-out). 
 */          
      
   private ConcurrentLinkedQueue<T> pool;  
         
 
    private ScheduledExecutorService executorService;  
      
       
    public ObjectPool(final int minObjects)   
    {  
        // initialize pool  
          
        initialize(minObjects);  
          
    }  
      
    /* 
      Creates the pool. 
      @param minObjects:   minimum number of objects residing in the pool. 
      @param maxObjects:   maximum number of objects residing in the pool. 
      @param validationInterval: time in seconds for periodical checking of  
         minObjects / maxObjects conditions in a separate thread. 
      When the number of objects is less than minObjects, missing instances will be created. 
      When the number of objects is greater than maxObjects, 
      too many instances will be removed. 
    */  
     public ObjectPool(final int minObjects, final int maxObjects, 
     final long validationInterval) {  
        // initialize pool  
         initialize(minObjects);  
          // check pool conditions in a separate thread  
        executorService = Executors.newSingleThreadScheduledExecutor();  
        executorService.scheduleWithFixedDelay(new Runnable()  // annonymous class  
        {  
            @Override  
            public void run() {  
                int size = pool.size();  
                 
                if (size < minObjects) {  
                    int sizeToBeAdded = minObjects + size;  
                    for (int i = 0; i < sizeToBeAdded; i++) {  
                        pool.add(createObject());  
                    }  
                } else if (size > maxObjects) {  
                    int sizeToBeRemoved = size - maxObjects;  
                    for (int i = 0; i < sizeToBeRemoved; i++) {  
                        pool.poll();  
                    }  
                }  
            }  
        }, validationInterval, validationInterval, TimeUnit.SECONDS);  
    }  
      
  /* 
      Gets the next free object from the pool. If the pool doesn't contain any objects, 
      a new object will be created and given to the caller of this method back. 
      
      @return T borrowed object 
  */  
    public T borrowObject() {  
        T object;  
        if ((object = pool.poll()) == null)  
        {  
            object = createObject();  
        }  
        return object;  
    }  
 /* 
      Returns object back to the pool. 
      @param object object to be returned 
  */  
    public void returnObject(T object) {  
        if (object == null) {  
            return;  
        }  
        this.pool.offer(object);  
    }  
   /* 
        Shutdown this pool. 
    */  
      public void shutdown(){  
        if (executorService != null){  
            executorService.shutdown();  
        }  
    }  
    /* 
        Creates a new object. 
         @return T new object 
     */  
    protected abstract T createObject();  
  
    private void initialize(final int minObjects)  {  
        pool = new ConcurrentLinkedQueue<T>();  
        for (int i = 0; i < minObjects; i++) {  
            pool.add(createObject());  
        }  
    }  
}// End of the ObjectPool Class. 
```

#### Create an ExportingProcess class

<br>

* Create an ExportingProcess class that will be used by ExportingTask class


**File: ExportingProcess.java**

```java
public class ExportingProcess {  
 private long processNo;  
  
    public ExportingProcess(long processNo)  {  
         this.processNo = processNo;  
        // do some  expensive calls / tasks here in future  
        // .........  
      System.out.println("Object with process no. " + processNo + " was created");  
     }  
     
    public long getProcessNo() {  
        return processNo;  
    }  
}// End of the ExportingProcess class.
```  

#### Create an ExportingTask class

<br>

* Create an ExportingTask class that will use ExportingProcess and ObjectPool class.

**File: ExportingTask.java**

```java
public class ExportingTask implements Runnable {  
        private ObjectPool<ExportingProcess> pool;  
        private int threadNo;  
        public ExportingTask(ObjectPool<ExportingProcess> pool, int threadNo){  
            this.pool = pool;  
            this.threadNo = threadNo;  
        }  
      
        public void run() {  
            // get an object from the pool  
            ExportingProcess exportingProcess = pool.borrowObject();  
            System.out.println("Thread " + threadNo + ": Object with process no. "  
                    + exportingProcess.getProcessNo() + " was borrowed");  
  
            //you can  do something here in future  
            // .........  
  
               // return ExportingProcess instance back to the pool  
            pool.returnObject(exportingProcess);  
  
            System.out.println("Thread " + threadNo +": Object with process no. "  
                   + exportingProcess.getProcessNo() + " was returned");  
        }  
  
    }// End of the ExportingTask class.
```   

#### Create an ObjectPoolDemo class

<br>

**File: ObjectPoolDemo.java**

```java
import java.util.concurrent.ExecutorService;  
import java.util.concurrent.Executors;  
import java.util.concurrent.TimeUnit;  
import java.util.concurrent.atomic.AtomicLong;  
public class ObjectPoolDemo{  
      private ObjectPool<ExportingProcess> pool;  
      private AtomicLong processNo=new AtomicLong(0);  
      public void setUp() {  
            // Create a pool of objects of type ExportingProcess.  
           /*Parameters: 
             1) Minimum number of special ExportingProcess instances residing in the pool = 4 
             2) Maximum number of special ExportingProcess instances residing in the pool = 10 
             3) Time in seconds for periodical checking of minObjects / maxObjects conditions 
                in a separate thread = 5. 
             -->When the number of ExportingProcess instances is less than minObjects,  
                 missing instances will be created. 
             -->When the number of ExportingProcess instances is greater than maxObjects, 
                  too many instances will be removed. 
            -->If the validation interval is negative, no periodical checking of  
                  minObjects / maxObjects conditions in a separate thread take place. 
              These boundaries are ignored then. 
           */  
      pool = new ObjectPool<ExportingProcess>(4, 10, 5)  
        {  
            protected ExportingProcess createObject()  
            {  
                // create a test object which takes some time for creation  
                return new ExportingProcess( processNo.incrementAndGet());  
            }  
        };  
    }  
    public void tearDown() {  
        pool.shutdown();  
    }  
    public void testObjectPool() {  
        ExecutorService executor = Executors.newFixedThreadPool(8);  
  
        // execute 8 tasks in separate threads  
          
        executor.execute(new ExportingTask(pool, 1));  
        executor.execute(new ExportingTask(pool, 2));  
        executor.execute(new ExportingTask(pool, 3));  
        executor.execute(new ExportingTask(pool, 4));  
        executor.execute(new ExportingTask(pool, 5));  
        executor.execute(new ExportingTask(pool, 6));  
        executor.execute(new ExportingTask(pool, 7));  
        executor.execute(new ExportingTask(pool, 8));  
  
        executor.shutdown();  
        try {  
            executor.awaitTermination(30, TimeUnit.SECONDS);  
            } catch (InterruptedException e)  
              
              {  
               e.printStackTrace();  
              }  
    }  
    public static void main(String args[])  {   
        ObjectPoolDemo op=new ObjectPoolDemo();  
        op.setUp();  
        op.tearDown();  
        op.testObjectPool();  
   }   
}//End of the ObjectPoolDemo class.
```  

#### Output

<br>

![output](images/dp15.png)



# Structural design patterns

<br>

* Structural design patterns are concerned with how classes and objects can be composed, to form larger structures.

* The structural design patterns simplifies the structure by identifying the relationships.

* These patterns focus on, how the classes inherit from each other and how they are composed from other classes.

<br>

<!-- style="font-size:20px;"--> 
**Types of structural design patterns**

There are following 7 types of structural design patterns.

<!-- style="font-size:20px;"-->
1. [Adapter Pattern](#adapter-pattern)
Adapting an interface into another according to client expectation.

<!-- style="font-size:20px;"-->
2. [Bridge Pattern](#bridge-pattern)
Separating abstraction (interface) from implementation.

<!-- style="font-size:20px;"-->
3. [Composite Pattern](#composite-pattern)
Allowing clients to operate on hierarchy of objects.

<!-- style="font-size:20px;"-->
4. [Decorator Pattern](#decorator-pattern)
Adding functionality to an object dynamically.

<!-- style="font-size:20px;"-->
5. [Facade Pattern](#facade-pattern)
Providing an interface to a set of interfaces.

<!-- style="font-size:20px;"-->
6. [Flyweight Pattern](#flyweight-pattern)
Reusing an object by sharing it.

<!-- style="font-size:20px;"-->
7. [proxy Pattern](#proxy-pattern)
Representing another object.

## Adapter Pattern

<br>

* An Adapter Pattern says that just "**converts the interface of a class into another interface that a client wants**".

* In other words, to provide the interface according to client requirement while using the services of a class with a different interface.

* The Adapter Pattern is also known as Wrapper.

<br>

<!-- style="font-size:20px;"-->
**Advantage of Adapter Pattern**

<br>

* It allows two or more previously incompatible objects to interact.
* It allows reusability of existing functionality.

<br>

<!-- style="font-size:20px;"-->
**Usage of Adapter pattern:**

<br>

* When an object needs to utilize an existing class with an incompatible interface.
* When you want to create a reusable class that cooperates with classes which don't have compatible interfaces.
* When you want to create a reusable class that cooperates with classes which don't have compatible interfaces.

### UML for Adapter Pattern:

<br>

The following are the specifications for the adapter pattern:

**Target Interface :** This is the desired interface class which will be used by the clients.

**Adapter class :** This class is a wrapper class which implements the desired target interface and modifies the specific request available from the Adaptee class.

**Adaptee class :** This is the class which is used by the Adapter class to reuse the existing functionality and modify them for desired use.

**Client :** This class will interact with the Adapter class.

<br>

![Uml](images/dp16.png)


### Example of Adapter Pattern

<br>

<!-- style="font-size:20px;"-->
1. [Create a CreditCard interface (Target interface).](#create-a-creditcard-interface)

<!-- style="font-size:20px;"-->
2. [Create a BankDetails class (Adaptee class).](#create-a-bankdetails-class)

<!-- style="font-size:20px;"-->
3. [Create a BankCustomer class (Adapter class).](#create-a-bankcustomer-class)

<!-- style="font-size:20px;"-->
4. [Create a AdapterPatternDemo class (client class).](#create-a-adapterpatterndemo-class)

#### Create a CreditCard interface

<br>

* Create a CreditCard interface (Target interface).

```java
public interface CreditCard {  
    public void giveBankDetails();  
    public String getCreditCard();  
}// End of the CreditCard interface. 
``` 

#### Create a BankDetails class

<br>

* Create a BankDetails class (Adaptee class).

**File: BankDetails.java**

```java
// This is the adapter class.  
public class BankDetails{  
    private String bankName;  
    private String accHolderName;  
    private long accNumber;  
      
    public String getBankName() {  
        return bankName;  
    }  
    public void setBankName(String bankName) {  
        this.bankName = bankName;  
    }  
    public String getAccHolderName() {  
        return accHolderName;  
    }  
    public void setAccHolderName(String accHolderName) {  
        this.accHolderName = accHolderName;  
    }  
    public long getAccNumber() {  
        return accNumber;  
    }  
    public void setAccNumber(long accNumber) {  
        this.accNumber = accNumber;  
    }  
}// End of the BankDetails class. 
``` 

#### Create a BankCustomer class

<br>

* Create a BankCustomer class (Adapter class).

**File: BankCustomer.java**

```java
// This is the adapter class  
  
import java.io.BufferedReader;  
import java.io.InputStreamReader;  
public class BankCustomer extends BankDetails implements CreditCard {  
 public void giveBankDetails(){  
  try{  
   BufferedReader br=new BufferedReader(new InputStreamReader(System.in));  
      
   System.out.print("Enter the account holder name :");  
   String customername=br.readLine();  
   System.out.print("\n");  
      
   System.out.print("Enter the account number:");  
   long accno=Long.parseLong(br.readLine());  
   System.out.print("\n");  
      
   System.out.print("Enter the bank name :");  
   String bankname=br.readLine();  
      
   setAccHolderName(customername);  
   setAccNumber(accno);  
   setBankName(bankname);  
   }catch(Exception e){  
        e.printStackTrace();  
   }  
  }  
  @Override  
  public String getCreditCard() {  
   long accno=getAccNumber();  
   String accholdername=getAccHolderName();  
   String bname=getBankName();  
          
   return ("The Account number "+accno+" of "+accholdername+" in "+bname+ "  
                        bank is valid and authenticated for issuing the credit card. ");  
  }  
}//End of the BankCustomer class.  
```

#### Create a AdapterPatternDemo class

<br>

* Create a AdapterPatternDemo class (client class).

**File: AdapterPatternDemo.java**

```java
//This is the client class.  
public class AdapterPatternDemo {  
 public static void main(String args[]){  
  CreditCard targetInterface=new BankCustomer();  
  targetInterface.giveBankDetails();  
  System.out.print(targetInterface.getCreditCard());  
 }   
}//End of the BankCustomer class. 
```

#### Output

<br>

![output](images/dp17.png)


## Bridge Pattern

<br>

* A Bridge Pattern says that just "decouple the functional abstraction from the implementation so that the two can vary independently".

* The Bridge Pattern is also known as Handle or Body.

<br>

<!--style="font-size:20px" -->
Advantage of Bridge Pattern

* It enables the separation of implementation from the interface.
* It improves the extensibility.
* It allows the hiding of implementation details from the client.

<br>

<!--style="font-size:20px" -->
Usage of Bridge Pattern

* When you don't want a permanent binding between the functional abstraction and its implementation.
* When both the functional abstraction and its implementation need to extended using sub-classes.
* It is mostly used in those places where changes are made in the implementation does not affect the clients.

### UML for Bridge Pattern

![Uml](images/dp18.png)


### Example of Bridge Pattern

<br>

<!--style="font-size:20px" -->
1. [Create a Question interface](#create-a-question-interface)

<!--style="font-size:20px" -->
2. [Create a JavaQuestions implementation](#create-a-javaquestions-implementation)

<!--style="font-size:20px" -->
3. [Create a QuestionManager class](#create-a-questionmanager-class)

<!--style="font-size:20px" -->
4. [Create a QuestionFormat class](#create-a-questionformat-class)

<!--style="font-size:20px" -->
5. [Create a BridgePatternDemo class](#create-a-bridgepatterndemo-class)

#### Create a Question interface

<br>

* Create a Question interface that provides the navigation from one question to another or vice-versa.

```java
// this is the Question interface.  
public interface Question {  
    public void nextQuestion();  
    public void previousQuestion();  
    public void newQuestion(String q);  
    public void deleteQuestion(String q);  
    public void displayQuestion();  
    public void displayAllQuestions();  
}  
// End of the Question interface. 
``` 

#### Create a JavaQuestions implementation

* Create a JavaQuestions implementation class that will implement Question interface.

```java
// this is the JavaQuestions class.  
import java.util.ArrayList;  
import java.util.List;  
public class JavaQuestions implements Question {  
 private List <String> questions = new ArrayList<String>();  
 private int current = 0;  
 public JavaQuestions(){  
    questions.add("What is class? ");  
    questions.add("What is interface? ");  
    questions.add("What is abstraction? ");  
    questions.add("How multiple polymorphism is achieved in java? ");  
    questions.add("How many types of exception  handling are there in java? ");  
    questions.add("Define the keyword final for  variable, method, and class in java? ");  
    questions.add("What is abstract class? ");  
    questions.add("What is multi-threading? ");  
 }  
 public void nextQuestion() {  
    if( current <= questions.size()-1 )  
    current++;  
    System.out.print(current);  
 }  
  
 public void previousQuestion() {  
    if( current > 0 )  
    current--;  
 }  
  
 public void newQuestion(String quest) {  
    questions.add(quest);  
 }  
  
 public void deleteQuestion(String quest) {  
    questions.remove(quest);  
 }  
  
 public void displayQuestion() {  
    System.out.println( questions.get(current) );  
 }  
 public void displayAllQuestions() {  
    for (String quest : questions) {  
    System.out.println(quest);  
 }  
}  
}// End of the JavaQuestions class.  
```

#### Create a QuestionManager class

<br>

* Create a QuestionManager class that will use Question interface which will act as a bridge..

```java
// this is the QuestionManager class.  
public class QuestionManager  {  
    protected Question q;  
    public String catalog;  
    public QuestionManager(String catalog) {  
    this.catalog=catalog;  
    }  
    public void next() {  
    q.nextQuestion();  
    }  
    public void previous() {  
    q.previousQuestion();  
    }  
    public void newOne(String quest) {  
    q.newQuestion(quest);  
    }  
    public void delete(String quest) {  
    q.deleteQuestion(quest);  
    }  
    public void display() {  
    q.displayQuestion();  
    }  
    public void displayAll() {  
        System.out.println("Question Paper: " + catalog);  
    q.displayAllQuestions();  
    }  
}// End of the QuestionManager class.  
```

#### Create a QuestionFormat class

<br>

* Create a QuestionFormat class that will extend the QuestionManager class

```java
// this is the QuestionFormat class.  
public class QuestionFormat extends QuestionManager {  
    public QuestionFormat(String catalog){  
        super(catalog);  
    }  
    public void displayAll() {  
        System.out.println("\n---------------------------------------------------------");  
        super.displayAll();  
        System.out.println("-----------------------------------------------------------");  
    }  
}// End of the QuestionFormat class.  
```

#### Create a BridgePatternDemo class

<br>

* Create a BridgePatternDemo class.

```java
// this is the BridgePatternDemo class.  
public class BridgePatternDemo {  
    public static void main(String[] args) {  
    QuestionFormat questions = new QuestionFormat("Java Programming Language");  
    questions.q = new JavaQuestions();  
        questions.delete("what is class?");  
        questions.display();  
    questions.newOne("What is inheritance? ");  
      
    questions.newOne("How many types of inheritance are there in java?");  
    questions.displayAll();  
    }  
}// End of the BridgePatternDemo class. 
``` 

#### Output

<br>

![output](images/dp19.png)


## Composite Pattern

<br>

A Composite Pattern says that just "allow clients to operate in generic manner on objects that may or may not represent a hierarchy of objects".

<!-- style="font-size:20px;"-->
Advantage of Composite Design Pattern

* It defines class hierarchies that contain primitive and complex objects.
* It makes easier to you to add new kinds of components.
* It provides flexibility of structure with manageable class or interface.

<br>

<!-- style="font-size:20px;"-->
Usage of Composite Pattern

**It is used:**

* When you want to represent a full or partial hierarchy of objects.
* When the responsibilities are needed to be added dynamically to the individual objects without affecting other objects. Where the responsibility of object may vary from time to time.

### UML for Composite Pattern

<br>

![Uml](images/dp20.png)

### Elements used in Composite Pattern:

<br>

**1. Component**

Declares interface for objects in composition.
Implements default behavior for the interface common to all classes as appropriate.
Declares an interface for accessing and managing its child components.

**2. Leaf**

Represents leaf objects in composition. A leaf has no children.
Defines behavior for primitive objects in the composition.

**3. Composite**

Defines behavior for components having children.
Stores child component.
Implements child related operations in the component interface.

**4. Client**

Manipulates objects in the composition through the component interface.

### Example of Composite Pattern

<br>

<!-- style="font-size:20px;"-->
1. [Create an Employee interface](#create-an-employee-interface)

<!-- style="font-size:20px;"-->
2. [Create a BankManager class](#create-a-bankmanager-class)  

<!-- style="font-size:20px;"-->
3. [Create a Cashier class](#create-a-cashier-class)

<!-- style="font-size:20px;"-->
4. [Create a Accountant class](#create-a-accountant-class)

<!-- style="font-size:20px;"-->
5. [Create a CompositePatternDemo class](#create-a-compositepatterndemo-class)


#### Create an Employee interface

<br>

* Create an Employee interface that will be treated as a component.

```java
// this is the Employee interface i.e. Component.  
public interface Employee {  
    public  int getId();  
    public String getName();  
    public double getSalary();  
       public void print();  
    public void add(Employee employee);  
       public void remove(Employee employee);  
       public Employee getChild(int i);  
}// End of the Employee interface. 
``` 

#### Create a BankManager class

<br>

* Create a BankManager class that will be treated as a Composite and implements Employee interface.

**File: BankManager.java**

```java
// this is the BankManager class i.e. Composite.  
import java.util.ArrayList;  
import java.util.Iterator;  
import java.util.List;  
public class BankManager implements Employee {  
     private int id;  
     private String name;  
     private double salary;  
  
     public BankManager(int id,String name,double salary) {  
      this.id=id;      
      this.name = name;  
      this.salary = salary;  
     }  
         List<Employee> employees = new ArrayList<Employee>();  
     @Override  
     public void add(Employee employee) {  
        employees.add(employee);  
     }  
        @Override  
     public Employee getChild(int i) {  
      return employees.get(i);  
     }  
     @Override  
     public void remove(Employee employee) {  
      employees.remove(employee);  
     }    
     @Override  
     public int getId()  {  
      return id;  
     }  
     @Override  
     public String getName() {  
      return name;  
     }  
    @Override  
     public double getSalary() {  
      return salary;  
     }  
     @Override  
     public void print() {  
      System.out.println("==========================");  
      System.out.println("Id ="+getId());  
      System.out.println("Name ="+getName());  
      System.out.println("Salary ="+getSalary());  
      System.out.println("==========================");  
        
      Iterator<Employee> it = employees.iterator();  
        
          while(it.hasNext())  {  
            Employee employee = it.next();  
            employee.print();  
         }  
     }  
}// End of the BankManager class.  
```

#### Create a Cashier class

<br>

* Create a Cashier class that will be treated as a leaf and it will implement to the Employee interface.

**File: Cashier.java** 

```java
public  class Cashier implements Employee{  
    /* 
         In this class,there are many methods which are not applicable to cashier because 
         it is a leaf node. 
     */  
        private int id;  
            private String name;  
        private double salary;  
        public Cashier(int id,String name,double salary)  {  
            this.id=id;  
            this.name = name;  
            this.salary = salary;  
        }  
        @Override  
        public void add(Employee employee) {  
            //this is leaf node so this method is not applicable to this class.  
        }  
        @Override  
        public Employee getChild(int i) {  
            //this is leaf node so this method is not applicable to this class.  
            return null;  
        }  
        @Override  
        public int getId() {  
            // TODO Auto-generated method stub  
            return id;  
        }  
        @Override  
        public String getName() {  
            return name;  
        }  
        @Override  
        public double getSalary() {  
            return salary;  
        }  
        @Override  
        public void print() {  
            System.out.println("==========================");  
            System.out.println("Id ="+getId());  
            System.out.println("Name ="+getName());  
            System.out.println("Salary ="+getSalary());  
            System.out.println("==========================");  
        }  
        @Override  
        public void remove(Employee employee) {  
            //this is leaf node so this method is not applicable to this class.  
        }  
}  
```

#### Create a Accountant class

<br>

Create a Accountant class that will also be treated as a leaf and it will implement to the Employee interface.

**File: Accountant.java**

```java
public class Accountant implements Employee{  
/* 
    In this class,there are many methods which are not applicable to cashier because 
    it is a leaf node. 
*/  
    private int id;  
    private String name;  
    private double salary;  
   public Accountant(int id,String name,double salary)  {  
       this.id=id;  
       this.name = name;  
       this.salary = salary;  
   }  
   @Override  
   public void add(Employee employee) {  
       //this is leaf node so this method is not applicable to this class.  
   }  
   @Override  
   public Employee getChild(int i) {  
       //this is leaf node so this method is not applicable to this class.  
       return null;  
   }  
   @Override  
    public int getId() {  
        // TODO Auto-generated method stub  
        return id;  
   }  
   @Override  
   public String getName() {  
       return name;  
   }  
   @Override  
   public double getSalary() {  
       return salary;  
   }  
   @Override  
   public void print() {  
       System.out.println("=========================");  
       System.out.println("Id ="+getId());  
       System.out.println("Name ="+getName());  
       System.out.println("Salary ="+getSalary());  
       System.out.println("=========================");  
   }  
  @Override  
   public void remove(Employee employee) {  
       //this is leaf node so this method is not applicable to this class.  
   }  
} 
``` 

#### Create a CompositePatternDemo class

<br>

* Create a CompositePatternDemo class that will also be treated as a Client and ii will use the Employee interface.

**File: CompositePatternDemo.java**

```java
public class CompositePatternDemo {  
    public static void main(String args[]){  
         Employee emp1=new Cashier(101,"Sohan Kumar", 20000.0);  
         Employee emp2=new Cashier(102,"Mohan Kumar", 25000.0);  
         Employee emp3=new Accountant(103,"Seema Mahiwal", 30000.0);   
         Employee manager1=new BankManager(100,"Ashwani Rajput",100000.0);  
            
          manager1.add(emp1);  
          manager1.add(emp2);  
          manager1.add(emp3);  
          manager1.print();  
        }  
}  
```

#### Output

<br>

![output](images/dp21.png)



## Decorator Pattern

<br>

* A Decorator Pattern says that just "attach a flexible additional responsibilities to an object dynamically".

* In other words, The Decorator Pattern uses composition instead of inheritance to extend the functionality of an object at runtime.

* The Decorator Pattern is also known as **Wrapper**.

<br>

<!-- style="font-size:20px;"-->
Advantage of Decorator Pattern

* It provides greater flexibility than static inheritance.
* It enhances the extensibility of the object, because changes are made by coding new classes.
* It simplifies the coding by allowing you to develop a series of functionality from targeted classes instead of coding all of the    behavior into the object.

<br>

<!-- style="font-size:20px;"-->
Usage of Decorator Pattern

**It is used:**

* When you want to transparently and dynamically add responsibilities to objects without affecting other objects.
* When you want to add responsibilities to an object that you may want to change in future.
* Extending functionality by sub-classing is no longer practical.

### UML for Decorator Pattern

<br>

![Uml](images/dp22.png)


### Example of Decorator Pattern

<br>

<!-- style="font-size:20px;"-->
1. [Create a Food interface](#create-a-food-interface)

<!-- style="font-size:20px;"-->
2. [Create a VegFood class](#create-a-vegfood-class)

<!-- style="font-size:20px;"-->
3. [Create a FoodDecorator abstract class](#create-a-fooddecorator-abstract-class)

<!-- style="font-size:20px;"-->
4. [Create a NonVegFood concrete class](#create-a-nonvegfood-concrete-class)

<!-- style="font-size:20px;"-->
5. [Create a ChineeseFood concrete class](#create-a-chineesefood-concrete-class)

<!-- style="font-size:20px;"-->
6. [Create a DecoratorPatternCustomer class](#create-a-decoratorpatterncustomer-class)


#### Create a Food interface

<br>

**Step 1 :** Create a Food interface.

```java
public interface Food {  
    public String prepareFood();  
    public double foodPrice();  
}// End of the Food interface.
``` 

#### Create a VegFood class

<br>

**Step 2 :** Create a VegFood class that will implements the Food interface and override its all methods.

**File: VegFood.java**

```java
public class VegFood implements Food {  
    public String prepareFood(){  
         return "Veg Food";  
    }  
  
        public double foodPrice(){  
        return 50.0;  
    }  
}  
```

#### Create a FoodDecorator abstract class

<br>

**Step 3 :** Create a FoodDecorator abstract class that will implements the Food interface and override it's all methods and it has the ability to decorate some more foods.

**File: FoodDecorator.java**

```java
public abstract class FoodDecorator implements Food{  
    private Food newFood;  
    public FoodDecorator(Food newFood)  {  
        this.newFood=newFood;  
    }  
    @Override  
    public String prepareFood(){  
        return newFood.prepareFood();   
    }  
    public double foodPrice(){  
        return newFood.foodPrice();  
    }  
}  

```
#### Create a NonVegFood concrete class

**Step 4 :** Create a NonVegFood concrete class that will extend the FoodDecorator class and override it's all methods.

**File: NonVegFood.java**

```java
public class NonVegFood extends FoodDecorator{    
    public NonVegFood(Food newFood) {  
        super(newFood);  
    }  
    public String prepareFood(){  
        return super.prepareFood() +" With Roasted Chiken and Chiken Curry  ";   
    }  
    public double foodPrice()   {  
        return super.foodPrice()+150.0;  
    }  
}  
```

#### Create a ChineeseFood concrete class

<br>

**Step 5 :** Create a ChineeseFood concrete class that will extend the FoodDecorator class and override it's all methods.

**File: ChineeseFood.java**

```java
public class ChineeseFood extends FoodDecorator{  
  public ChineeseFood(Food newFood)    {  
        super(newFood);  
  }  
    public String prepareFood(){  
        return super.prepareFood() +" With Fried Rice and Manchurian  ";   
    }  
    public double foodPrice()   {  
        return super.foodPrice()+65.0;  
        }  
} 
``` 

#### Create a DecoratorPatternCustomer class 

<br>

**Step 6 :** Create a DecoratorPatternCustomer class that will use Food interface to use which type of food customer wants means (Decorates).

**File: DecoratorPatternCustomer.java**

```java
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStreamReader;  
public class DecoratorPatternCustomer {  
    private static int  choice;  
    public static void main(String args[]) throws NumberFormatException, IOException    {  
       do{        
        System.out.print("========= Food Menu ============ \n");  
        System.out.print("            1. Vegetarian Food.   \n");  
        System.out.print("            2. Non-Vegetarian Food.\n");  
        System.out.print("            3. Chineese Food.         \n");  
        System.out.print("            4. Exit                        \n");  
        System.out.print("Enter your choice: ");  
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));   
        choice=Integer.parseInt(br.readLine());  
        switch (choice) {  
        case 1:{   
                 VegFood vf=new VegFood();  
              System.out.println(vf.prepareFood());  
              System.out.println( vf.foodPrice());  
            }  
            break;  
              
                case 2:{  
                Food f1=new NonVegFood((Food) new VegFood());  
                    System.out.println(f1.prepareFood());  
                System.out.println( f1.foodPrice());  
        }  
            break;    
     case 3:{  
             Food f2=new ChineeseFood((Food) new VegFood());  
                     System.out.println(f2.prepareFood());  
                    System.out.println( f2.foodPrice());  
              }  
            break;    
              
         default:{    
            System.out.println("Other than these no food available");  
        }         
    return;  
     }//end of switch  
          
}while(choice!=4);  
    }  
}
```  

#### Output

<br>

![output](images/dp23.png)

## Facade Pattern

<br>

* A Facade Pattern says that just "just provide a unified and simplified interface to a set of interfaces in a subsystem, therefore it hides the complexities of the subsystem from the client".

* In other words, Facade Pattern describes a higher-level interface that makes the sub-system easier to use.

* Practically, every Abstract Factory is a type of Facade.

<br>

<!-- style="font-size:20px;"-->
Advantage of Facade Pattern

* It shields the clients from the complexities of the sub-system components.
* It promotes loose coupling between subsystems and its clients.

<br>

<!-- style="font-size:20px;"-->
Usage of Facade Pattern:

**It is used:**

* When you want to provide simple interface to a complex sub-system.
* When several dependencies exist between clients and the implementation classes of an abstraction.

### UML for Facade Pattern

<br>

![Uml](images/dp24.png)


### Example of Facade Pattern

<br>

<!-- style="font-size:20px;"-->
1. [Create a MobileShop interface](#create-a-mobileshop-interface)

<!-- style="font-size:20px;"-->
2. [Create a Iphone implementation class](#create-a-iphone-implementation-class)

<!-- style="font-size:20px;"-->
3. [Create a Samsung implementation class](#create-a-samsung-implementation-class)

<!-- style="font-size:20px;"-->
4. [Create a Blackberry implementation class](#create-a-blackberry-implementation-class)

<!-- style="font-size:20px;"-->
5. [Create a ShopKeeper concrete class](#create-a-shopkeeper-concrete-class)

<!-- style="font-size:20px;"-->
6. [Create a client](#create-a-client)


#### Create a MobileShop interface

<br>

* Create a MobileShop interface.

**File: MobileShop.java**

```java
public interface MobileShop {  
    public void modelNo();  
    public void price();  
}  
```

#### Create a Iphone implementation class

<br>

* Create a Iphone implementation class that will implement Mobileshop interface.

**File: Iphone.java**

```java
public class Iphone implements MobileShop {  
    @Override  
    public void modelNo() {  
        System.out.println(" Iphone 6 ");  
    }  
    @Override  
    public void price() {  
    System.out.println(" Rs 65000.00 ");  
    }  
} 
``` 

#### Create a Samsung implementation class

<br>

* Create a Samsung implementation class that will implement Mobileshop interface.

**File: Samsung.java**

```java
public class Samsung implements MobileShop {  
    @Override  
    public void modelNo() {  
    System.out.println(" Samsung galaxy tab 3 ");  
    }  
    @Override  
    public void price() {  
        System.out.println(" Rs 45000.00 ");  
    }  
} 
``` 

#### Create a Blackberry implementation class

<br>

* Create a Blackberry implementation class that will implement Mobileshop interface .

**File: Blackberry.java**

```java
public class Blackberry implements MobileShop {  
    @Override  
    public void modelNo() {  
    System.out.println(" Blackberry Z10 ");  
    }  
    @Override  
    public void price() {  
        System.out.println(" Rs 55000.00 ");  
    }  
} 
``` 

#### Create a ShopKeeper concrete class

<br>

* Create a ShopKeeper concrete class that will use MobileShop interface.

**File: ShopKeeper.java**

```java
public class ShopKeeper {  
    private MobileShop iphone;  
    private MobileShop samsung;  
    private MobileShop blackberry;  
      
    public ShopKeeper(){  
        iphone= new Iphone();  
        samsung=new Samsung();  
        blackberry=new Blackberry();  
    }  
    public void iphoneSale(){  
        iphone.modelNo();  
        iphone.price();  
    }  
        public void samsungSale(){  
        samsung.modelNo();  
        samsung.price();  
    }  
   public void blackberrySale(){  
    blackberry.modelNo();  
    blackberry.price();  
        }  
}  
```

#### Create a client

<br>

* Create client that can purchase the mobiles from MobileShop through ShopKeeper.

**File: FacadePatternClient.java**

```java
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStreamReader;  
  
public class FacadePatternClient {  
    private static int  choice;  
    public static void main(String args[]) throws NumberFormatException, IOException{  
        do{       
            System.out.print("========= Mobile Shop ============ \n");  
            System.out.print("            1. IPHONE.              \n");  
            System.out.print("            2. SAMSUNG.              \n");  
            System.out.print("            3. BLACKBERRY.            \n");  
            System.out.print("            4. Exit.                     \n");  
            System.out.print("Enter your choice: ");  
              
            BufferedReader br=new BufferedReader(new InputStreamReader(System.in));  
            choice=Integer.parseInt(br.readLine());  
            ShopKeeper sk=new ShopKeeper();  
              
            switch (choice) {  
            case 1:  
                {   
                  sk.iphoneSale();  
                    }  
                break;  
       case 2:  
                {  
                  sk.samsungSale();        
                    }  
                break;    
       case 3:  
                           {  
                           sk.blackberrySale();       
                           }  
                   break;     
            default:  
            {    
                System.out.println("Nothing You purchased");  
            }         
                return;  
            }  
              
      }while(choice!=4);  
   }  
}  
```

#### Output

<br>

![output](images/dp25.png)


## Flyweight Pattern

<br>

A Flyweight Pattern says that just "**to reuse already existing similar kind of objects by storing them and create new object when no matching object is found**".

<br>

<!-- style="font-size:20px;"-->
Advantage of Flyweight Pattern

* It reduces the number of objects.
* It reduces the amount of memory and storage devices required if the objects are persisted

<br>

<!-- style="font-size:20px;"-->
Usage of Flyweight Pattern

* When an application uses number of objects
* When the storage cost is high because of the quantity of objects.
* When the application does not depend on object identity.

## Proxy Pattern

<br>

* Proxy means an object representing another object.

* According to GoF, a Proxy Pattern "provides the control for accessing the original object".

* So, we can perform many operations like hiding the information of original object, on demand loading etc.

* Proxy pattern is also known as **Surrogate** or **Placeholder**.

<br>

<!-- style="font-size:20px;"-->
Advantage of Proxy Pattern

* It provides the protection to the original object from the outside world.

<br>

<!-- style="font-size:20px;"-->
Usage of Proxy Pattern:


* **It can be used in Virtual Proxy scenario** - Consider a situation where there is multiple database call to extract huge size image. Since this is an expensive operation so here we can use the proxy pattern which would create multiple proxies and point to the huge size memory consuming object for further processing. The real object gets created only when a client first requests/accesses the object and after that we can just refer to the proxy to reuse the object. This avoids duplication of the object and hence saving memory.

* **It can be used in Protective Proxy scenario** - It acts as an authorization layer to verify that whether the actual user has access the appropriate content or not. For example, a proxy server which provides restriction on internet access in office. Only the websites and contents which are valid will be allowed and the remaining ones will be blocked.

* **It can be used in Remote Proxy scenario** - A remote proxy can be thought about the stub in the RPC call. The remote proxy provides a local representation of the object which is present in the different address location. Another example can be providing interface for remote resources such as web service or REST resources.

* **It can be used in Smart Proxy scenario** - A smart proxy provides additional layer of security by interposing specific actions when the object is accessed. For example, to check whether the real object is locked or not before accessing it so that no other objects can change it.

### UML for Proxy Pattern

<br>

![Uml](images/dp26.png)

### Example of Proxy Pattern

<br>

<!-- style="font-size:20px;"-->
1. [Create an OfficeInternetAccess interface](#create-an-officeinternetaccess-interface)

<!-- style="font-size:20px;"-->
2. [Create a RealInternetAccess class](#create-a-realinternetaccess-class)

<!-- style="font-size:20px;"-->
3. [Create a ProxyInternetAccess class](#create-a-proxyinternetaccess-class)

<!-- style="font-size:20px;"-->
4. [Create a ProxyPatternClient class](#create-a-proxypatternclient-class)



#### Create an OfficeInternetAccess interface

<br>

```java
public interface OfficeInternetAccess {  
    public void grantInternetAccess();  
}
```

#### Create a RealInternetAccess class

<br>

* Create a RealInternetAccess class that will implement OfficeInternetAccess interface for granting the permission to the specific employee.

**File: RealInternetAccess.java**

```java
public class RealInternetAccess implements OfficeInternetAccess {  
    private String employeeName;  
    public RealInternetAccess(String empName) {  
        this.employeeName = empName;  
    }  
    @Override  
    public void grantInternetAccess() {  
        System.out.println("Internet Access granted for employee: "+ employeeName);  
    }  
}
```  

#### Create a ProxyInternetAccess class

<br>

* Create a ProxyInternetAccess class that will implement OfficeInternetAccess interface for providing the object of RealInternetAccess class.

**File: ProxyInternetAccess.java**

```java
public class ProxyInternetAccess implements OfficeInternetAccess {  
           private String employeeName;  
           private RealInternetAccess  realaccess;  
               public ProxyInternetAccess(String employeeName) {  
            this.employeeName = employeeName;  
        }  
        @Override  
        public void grantInternetAccess()   
        {  
            if (getRole(employeeName) > 4)   
            {  
                realaccess = new RealInternetAccess(employeeName);  
                realaccess.grantInternetAccess();  
            }   
            else   
            {  
                System.out.println("No Internet access granted. Your job level is below 5");  
            }  
        }  
        public int getRole(String emplName) {  
            // Check role from the database based on Name and designation  
            // return job level or job designation.  
            return 9;  
        }  
} 
``` 

#### Create a ProxyPatternClient class

<br>

* Create a ProxyPatternClient class that can access the internet actually.

**File: ProxyPatternClient.java**

```java
public class ProxyPatternClient {  
    public static void main(String[] args)   
    {  
        OfficeInternetAccess access = new ProxyInternetAccess("Ashwani Rajput");  
        access.grantInternetAccess();  
    }  
} 
``` 

#### Output

<br>

![output](images/dp27.png)


# Behavioral Design Patterns

<br>

* Behavioral design patterns are concerned with the interaction and responsibility of objects.

* In these design patterns, the interaction between the objects should be in such a way that they can easily talk to each other and still should be loosely coupled.

* That means the implementation and the client should be loosely coupled in order to avoid hard coding and dependencies.

<br>

<!-- style="font-size:20px;"-->
**There are 12 types of behavioral design patterns:**

<!-- style="font-size:20px;"-->
1. [Chain of Responsibility Pattern](#chain-of-responsibility-pattern)

<!-- style="font-size:20px;"-->
2. [Command Pattern](#command-pattern)

<!-- style="font-size:20px;"-->
3. [Interpreter Pattern](#interpreter-pattern)

<!-- style="font-size:20px;"-->
4. [Iterator Pattern](#iterator-pattern)

<!-- style="font-size:20px;"-->
5. [Mediator Pattern](#mediator-pattern)

<!-- style="font-size:20px;"-->
6. [Memento Pattern](#memento-pattern)

<!-- style="font-size:20px;"-->
7. [Observer Pattern](#observer-pattern)

<!-- style="font-size:20px;"-->
8. [State Pattern](#state-pattern)

<!-- style="font-size:20px;"-->
9. [Strategy Pattern](#strategy-pattern)

<!-- style="font-size:20px;"-->
10. [Template Pattern](#template-pattern)



## Chain of Responsibility Pattern

<br>

* In chain of responsibility, sender sends a request to a chain of objects. The request can be handled by any object in the chain.

* A Chain of Responsibility Pattern says that just "avoid coupling the sender of a request to its receiver by giving multiple objects a chance to handle the request". For example, an ATM uses the Chain of Responsibility design pattern in money giving process.

* In other words, we can say that normally each receiver contains reference of another receiver. If one object cannot handle the request then it passes the same to the next receiver and so on.

<br>

<!-- style="font-size:20px;"-->
Advantage of Chain of Responsibility Pattern

* It reduces the coupling.
* It adds flexibility while assigning the responsibilities to objects.
* It allows a set of classes to act as one; events produced in one class can be sent to other handler classes with the help of composition.

<br>

<!-- style="font-size:20px;"-->
Usage of Chain of Responsibility Pattern:

**It is used:**

* When more than one object can handle a request and the handler is unknown.
* When the group of objects that can handle the request must be specified in dynamic way.

### UML for Chain of Responsibility Pattern

<br>

![Uml](images/dp28.png)


### Example of Chain of Responsibility Pattern

<br>

<!-- style="font-size:20px;"-->
1. [Create a Logger abstract class](#create-a-logger-abstract-class)

<!-- style="font-size:20px;"-->
2. [Create a ConsoleBasedLogger class](#create-a-consolebasedlogger-class)

<!-- style="font-size:20px;"-->
3. [Create a DebugBasedLogger class](#create-a-debugbasedlogger-class)

<!-- style="font-size:20px;"-->
4. [Create a ErrorBasedLogger class](#create-a-errorbasedlogger-class)

<!-- style="font-size:20px;"-->
5. [Create a ChainOfResponsibilityClient class](#create-a-chainofresponsibilityclient-class)


#### Create a Logger abstract class

<br>

```java
public abstract class Logger {  
    public static int OUTPUTINFO=1;  
    public static int ERRORINFO=2;  
    public static int DEBUGINFO=3;  
    protected int levels;  
    protected Logger nextLevelLogger;  
    public void setNextLevelLogger(Logger nextLevelLogger) {  
        this.nextLevelLogger = nextLevelLogger;  
    }  
        public void logMessage(int levels, String msg){  
        if(this.levels<=levels){  
            displayLogInfo(msg);  
        }  
        if (nextLevelLogger!=null) {  
            nextLevelLogger.logMessage(levels, msg);  
        }  
    }  
    protected abstract void displayLogInfo(String msg);  
}  
```

#### Create a ConsoleBasedLogger class

<br>

**File: ConsoleBasedLogger.java**

```java
public class ConsoleBasedLogger extends Logger {  
    public ConsoleBasedLogger(int levels) {  
        this.levels=levels;  
    }  
    @Override  
    protected void displayLogInfo(String msg) {  
        System.out.println("CONSOLE LOGGER INFO: "+msg);  
    }  
} 
```

#### Create a DebugBasedLogger class

<br>

**File: DebugBasedLogger.java**

```java
public class DebugBasedLogger extends Logger {  
    public DebugBasedLogger(int levels) {  
        this.levels=levels;  
    }  
    @Override  
    protected void displayLogInfo(String msg) {  
        System.out.println("DEBUG LOGGER INFO: "+msg);  
    }  
}// End of the DebugBasedLogger class
```  

#### Create a ErrorBasedLogger class

<br>

**File: ErrorBasedLogger.java**

```java
public class ErrorBasedLogger extends Logger {  
    public ErrorBasedLogger(int levels) {  
        this.levels=levels;  
    }  
    @Override  
    protected void displayLogInfo(String msg) {  
        System.out.println("ERROR LOGGER INFO: "+msg);  
    }  
}// End of the ErrorBasedLogger class.
```  

#### Create a ChainOfResponsibilityClient class

<br>

**File: ChainofResponsibilityClient.java**

```java
public class ChainofResponsibilityClient {  
    private static Logger doChaining(){  
          Logger consoleLogger = new ConsoleBasedLogger(Logger.OUTPUTINFO);  
            
          Logger errorLogger = new ErrorBasedLogger(Logger.ERRORINFO);  
          consoleLogger.setNextLevelLogger(errorLogger);  
            
          Logger debugLogger = new DebugBasedLogger(Logger.DEBUGINFO);  
          errorLogger.setNextLevelLogger(debugLogger);  
            
          return consoleLogger;   
          }  
          public static void main(String args[]){  
          Logger chainLogger= doChaining();  
  
              chainLogger.logMessage(Logger.OUTPUTINFO, "Enter the sequence of values ");  
              chainLogger.logMessage(Logger.ERRORINFO, "An error is occured now");  
              chainLogger.logMessage(Logger.DEBUGINFO, "This was the error now debugging is compiled");  
              }  
}  
```

#### Output

<br>

![output](images/dp29.png)



## Command Pattern

<br>

* A Command Pattern says that "encapsulate a request under an object as a command and pass it to invoker object. Invoker object looks for the appropriate object which can handle this command and pass the command to the corresponding object and that object executes the command".

* It is also known as Action or Transaction.

<br>

<!-- style="font-size:20px;"-->
Advantage of command pattern

* It separates the object that invokes the operation from the object that actually performs the operation.
* It makes easy to add new commands, because existing classes remain unchanged.

<br>

<!-- style="font-size:20px;"-->
Usage of command pattern:

**It is used:**

* When you need parameterize objects according to an action perform.
* When you need to create and execute requests at different times.
* When you need to support rollback, logging or transaction functionality.

### UML for command pattern

<br>

* **Command** This is an interface for executing an operation.
* ConcreteCommand This class extends the Command interface and implements the execute method. This class creates a binding between the action and the receiver.
* **Client** This class creates the ConcreteCommand class and associates it with the receiver.
* **Invoker** This class asks the command to carry out the request.
* **Receiver** This class knows to perform the operation.

<br>

![Uml](images/dp30.png)


### Example of command pattern

<br>

<!-- style="font-size:20px;"-->
1. [Create a ActionListernerCommand](#create-a-actionlisternercommand)

<!-- style="font-size:20px;"-->
2. [Create a Document class](#create-a-document-class)

<!-- style="font-size:20px;"-->
3. [Create a ActionOpen class](#create-a-actionopen-class)

<!-- style="font-size:20px;"-->
4. [Create a ActionSave class](#create-a-actionsave-class)

<!-- style="font-size:20px;"-->
5. [Create a MenuOptions class](#create-a-menuoptions-class)

<!-- style="font-size:20px;"-->
6. [Create a CommanPatternClient class](#create-a-commanpatternclient-class)


#### Create a ActionListernerCommand

<br>

* Create a ActionListernerCommand interface that will act as a Command.

```java
public interface ActionListenerCommand {  
    public void execute();  
}
```  

#### Create a Document class

<br>

* Create a Document class that will act as a Receiver.

**File: Document.java**

```java
public class Document {  
          public void open(){  
           System.out.println("Document Opened");  
       }  
       public void save(){  
           System.out.println("Document Saved");  
       }  
} 
``` 

#### Create a ActionOpen class

<br>

* Create a ActionOpen class that will act as an ConcreteCommand.

**File: ActionOpen.java**

```java
public class ActionOpen implements ActionListenerCommand{  
    private Document doc;  
    public ActionOpen(Document doc) {  
        this.doc = doc;  
    }  
    @Override  
    public void execute() {  
        doc.open();  
    }  
}  
```

#### Create a ActionSave class

<br>

* Create a ActionSave class that will act as an ConcreteCommand.

**File: AdapterPatternDemo.java**

```java
public class ActionSave implements ActionListenerCommand{  
   private Document doc;  
   public ActionSave(Document doc) {  
        this.doc = doc;  
    }  
    @Override  
    public void execute() {  
        doc.save();  
    }  
}  
```

#### Create a MenuOptions class

<br>

* Create a MenuOptions class that will act as an Invoker.

**File: ActionSave.java**

```java
public class ActionSave implements ActionListenerCommand{  
   private Document doc;  
    public ActionSave(Document doc) {  
        this.doc = doc;  
    }  
    @Override  
    public void execute() {  
        doc.save();  
    }  
}  
```

#### Create a CommanPatternClient class

<br>

* Create a CommanPatternClient class that will act as a Client.

```java
**File: AdapterPatternDemo.java**

public class CommandPatternClient {  
    public static void main(String[] args) {  
        Document doc = new Document();  
          
        ActionListenerCommand clickOpen = new ActionOpen(doc);  
        ActionListenerCommand clickSave = new ActionSave(doc);  
          
        MenuOptions menu = new MenuOptions(clickOpen, clickSave);  
          
        menu.clickOpen();  
        menu.clickSave();  
   }  
} 
``` 

#### Output 

<br>

![Output](images/dp31.png)




## Interpreter Pattern

<br>

* An Interpreter Pattern says that "to define a representation of grammar of a given language, along with an interpreter that uses this representation to interpret sentences in the language".

* Basically the Interpreter pattern has limited area where it can be applied. 

* This pattern can applied for parsing the expressions defined in simple grammars and sometimes in simple rule engines.

<br>

<!-- style="font-size:20px;"-->
Advantage of Interpreter Pattern

* It is easier to change and extend the grammar.
* Implementing the grammar is straightforward.

<br>

<!-- style="font-size:20px;"-->
 Usage of Interpreter pattern:

 
**It is used:**

* When the grammar of the language is not complicated.
* When the efficiency is not a priority.


### UML for Interpreter Pattern

<br>

![Uml](images/dp32.png)


### Example of Interpreter Pattern

<br>

<!-- style="font-size:20px;"-->
1. [Create a Pattern interface](#create-a-pattern-interface)

<!-- style="font-size:20px;"-->
2. [Create a InfixToPostfixPattern class](#create-a-infixtopostfixpattern-class)

<!-- style="font-size:20px;"-->
3. [Create a InterpreterPatternClient class](#create-a-interpreterpatternclient-class)


#### Create a Pattern interface

<br>

```java
public interface Pattern {  
    public String conversion(String exp);  
} 
``` 

#### Create a InfixToPostfixPattern class

<br>

* Create a InfixToPostfixPattern class that will allow what kind of pattern you want to convert.

**File: InfixToPostfixPattern.java**

```java
import java.util.Stack;  
public class InfixToPostfixPattern implements Pattern{  
    @Override  
    public String conversion(String exp) {  
        int priority = 0;// for the priority of operators.  
       String postfix = "";  
        Stack<Character> s1 = new Stack<Character>();  
       for (int i = 0; i < exp.length(); i++)  
        {  
           char ch = exp.charAt(i);  
           if (ch == '+' || ch == '-' || ch == '*' || ch == '/'||ch=='%')  
           {  
              // check the precedence  
              if (s1.size() <= 0)  
                 s1.push(ch);  
           }  
           else  
              {  
                 Character chTop = (Character) s1.peek();  
                 if (chTop == '*' || chTop == '/')  
                    priority = 1;  
                 else  
                    priority = 0;  
                 if (priority == 1)  
                 {  
                    if (ch == '*' || ch == '/'||ch=='%')  
                    {  
                       postfix += s1.pop();  
                                                  i--;  
                    }  
                    else  
                    { // Same  
                       postfix += s1.pop();  
                       i--;  
                    }  
                 }  
                 else  
                 {  
                    if (ch == '+' || ch == '-')  
                    {  
                       postfix += s1.pop();  
                       s1.push(ch);  
                    }  
                    else  
                       s1.push(ch);  
                 }  
              }  
           }  
           else  
           {               
              postfix += ch;  
           }  
        }  
        int len = s1.size();  
        for (int j = 0; j < len; j++)  
           postfix += s1.pop();  
        return postfix;  
          
    }   
}// End of the InfixToPostfixPattern class. 
``` 

#### Create a InterpreterPatternClient class

<br>

* Create a InterpreterPatternClient class that will use InfixToPostfix Conversion.

**File: InterpreterPatternClient.java**

```java
public class InterpreterPatternClient {  
     public static void main(String[] args)  
        {  
            String infix = "a+b*c";  
              
            InfixToPostfixPattern ip=new InfixToPostfixPattern();  
              
            String postfix = ip.conversion(infix);  
            System.out.println("Infix:   " + infix);  
            System.out.println("Postfix: " + postfix);  
       }  
}  
```

#### Output

<br>

![output](images/dp33.png)


## Iterator Pattern

<br>

* Iterator Pattern is used "**to access the elements of an aggregate object sequentially without exposing its underlying implementation**".

* The Iterator pattern is also known as **Cursor**.

In collection framework, we are now using Iterator that is preferred over Enumeration.

```
java.util.Iterator interface uses Iterator Design Pattern
```
<br>

<!-- style="font-size:20px;"-->
Advantage of Iterator Pattern

* It supports variations in the traversal of a collection.
* It simplifies the interface to the collection.

<br>

<!-- style="font-size:20px;"-->
Usage of Iterator Pattern:

**It is used:**

* When you want to access a collection of objects without exposing its internal representation.
* When there are multiple traversals of objects need to be supported in the collection.


### UML for Iterator Pattern

<br>

![Uml](images/dp34.png)


### Example of Iterator Pattern

<br>

<!-- style="font-size:20px;"-->
1. [Create a Iterartor interface](#create-a-iterartor-interface)

<!-- style="font-size:20px;"-->
2. [Create a Container interface](#create-a-container-interface)

<!-- style="font-size:20px;"-->
3. [Create a CollectionofNames class](#create-a-collectionofnames-class)

<!-- style="font-size:20px;"-->
4. [Create a IteratorPatternDemo class](#create-a-iteratorpatterndemo-class)


#### Create a Iterartor interface

<br>

```java
public interface Iterator {  
    public boolean hasNext();  
    public Object next();  
} 
``` 

#### Create a Container interface

<br>

```java
public interface Container {  
    public Iterator getIterator();  
}// End of the Iterator interface.
```  

#### Create a CollectionofNames class

<br>

* Create a CollectionofNames class that will implement Container interface.

**File: CollectionofNames.java**

```java
public class CollectionofNames implements Container {  
public String name[]={"Ashwani Rajput", "Soono Jaiswal","Rishi Kumar","Rahul Mehta","Hemant Mishra"};   
      
@Override  
    public Iterator getIterator() {  
        return new CollectionofNamesIterate() ;  
    }  
    private class CollectionofNamesIterate implements Iterator{  
        int i;  
        @Override  
        public boolean hasNext() {  
            if (i<name.length){  
                return true;  
            }  
            return false;  
        }  
        @Override  
        public Object next() {  
            if(this.hasNext()){  
                return name[i++];  
            }  
            return null;      
        }  
    }  
}  
}
```  

#### Create a IteratorPatternDemo class

<br>

* Create a IteratorPatternDemo class.

**File: IteratorPatternDemo.java**

```java
public class IteratorPatternDemo {  
    public static void main(String[] args) {  
          CollectionofNames cmpnyRepository = new CollectionofNames();  
            
          for(Iterator iter = cmpnyRepository.getIterator(); iter.hasNext();){  
              String name = (String)iter.next();  
              System.out.println("Name : " + name);  
           }      
    }  
}
```  

#### Output

<br>

![output](images/dp35.png)


## Mediator Pattern

<br>

* A Mediator Pattern says that "to define an object that encapsulates how a set of objects interact".

* The logic becomes more complex when functionality increases. Then what happens? We add more classes and they still interact with each other but it gets really difficult to maintain this code now. So, Mediator pattern takes care of this problem.

* pattern is used to reduce communication complexity between multiple objects or classes. This pattern provides a mediator class which normally handles all the communications between different classes and supports easy maintainability of the code by loose coupling.

<!-- style="font-size:20px;"-->
Advantages:

* It decouples the number of classes.
* It simplifies object protocols.
* It centralizes the control.
* The individual components become simpler and much easier to deal with because they don't need to pass messages to one another.
* The components don't need to contain logic to deal with their intercommunication and therefore, they are more generic.

<!-- style="font-size:20px;"-->
Usage:

* It is commonly used in message-based systems likewise chat applications.
* When the set of objects communicate in complex but in well-defined ways.

### UML for Mediator Pattern

<br>

![Uml](images/dp36.png)

<br>

**ApnaChatroom :** defines the interface for interacting with participants.

**ApnaChatroomImpl :** implements the operations defined by the Chatroom interface. The operations are managing the interactions between the objects: when one participant sends a message, the message is sent to the other participants.

**Participant :** defines an interface for the users involved in chatting.

**User1, User2, ...UserN :** implements Participant interface; the participant can be a number of users involved in chatting. But each Participant will keep only a reference to the ApnaChatRoom.

### Example of Mediator Pattern

<br>

<!-- style="font-size:20px;"-->
1. [Create a ApnaChatRoom interface](#create-a-apnachatroom-interface)

<!-- style="font-size:20px;"-->
2. [Create a ApnaChatRoomIml class](#create-a-apnachatroomiml-class)

<!-- style="font-size:20px;"-->
3. [Create a Participant abstract class](#create-a-participant-abstract-class)

<!-- style="font-size:20px;"-->
4. [Create a User1 class](#create-a-user1-class)

<!-- style="font-size:20px;"-->
5. [Create a User2 class](#create-a-user2-class)

<!-- style="font-size:20px;"-->
6. [Create a MediatorPatternDemo class](#create-a-mediatorpatterndemo-class)


#### Create a ApnaChatRoom interface

<br>


```java
//This is an interface.  
public interface ApnaChatRoom {  
      
    public void showMsg(String msg, Participant p);  
  
}// End of the ApnaChatRoom interface.
```  

#### Create a ApnaChatRoomIml class

<br>


* Create a ApnaChatRoomIml class that will implement ApnaChatRoom interface and will also use the number of participants involved in chatting through Participant interface.


```java
//This is a class.  
import java.text.DateFormat;  
import java.text.SimpleDateFormat;  
import java.util.Date;  
  
public class ApnaChatRoomImpl implements ApnaChatRoom{  
    //get current date time   
    DateFormat dateFormat = new SimpleDateFormat("E dd-MM-yyyy hh:mm a");  
    Date date = new Date();  
    @Override  
    public void showMsg(String msg, Participant p) {  
          
        System.out.println(p.getName()+"'gets message: "+msg);  
        System.out.println("\t\t\t\t"+"["+dateFormat.format(date).toString()+"]");    
    }     
}// End of the ApnaChatRoomImpl class.
```  

#### Create a Participant abstract class

<br>

```java
//This is an abstract class.  
public abstract class Participant {  
      public abstract void sendMsg(String msg);  
      public abstract void setname(String name);  
      public abstract String getName();  
}// End of the Participant abstract class. 
``` 

#### Create a User1 class

<br>

* Create a User1 class that will extend Participant abstract class and will use the ApnaChatRoom interface.

```java
//This is a class.  
  
public class User1 extends Participant {  
      
    private String name;  
    private ApnaChatRoom chat;  
      
    @Override  
    public void sendMsg(String msg) {  
    chat.showMsg(msg,this);  
          
    }  
  
    @Override  
    public void setname(String name) {  
        this.name=name;  
    }  
  
    @Override  
    public String getName() {  
        return name;  
    }  
      
    public User1(ApnaChatRoom chat){  
        this.chat=chat;  
    }     
      
}// End of the User1 class.  
```

#### Create a User2 class

<br>

* Create a User2 class that will extend Participant abstract class and will use the ApnaChatRoom interface.

//This is a class.  
  
```java
public class User2 extends Participant {  
  
    private String name;  
    private ApnaChatRoom chat;  
      
    @Override  
    public void sendMsg(String msg) {  
    this.chat.showMsg(msg,this);  
          
    }  
  
    @Override  
    public void setname(String name) {  
        this.name=name;  
    }  
  
    @Override  
    public String getName() {  
        return name;  
    }  
      
    public User2(ApnaChatRoom chat){  
        this.chat=chat;  
    }  
  
      
      
}  
// End of the User2 class. 
``` 

#### Create a MediatorPatternDemo class

<br>

* Create a MediatorPatternDemo class that will use participants involved in chatting.

```java
//This is a class.  
  
public class MediatorPatternDemo {  
      
    public static void main(String args[])  
    {  
          
          ApnaChatRoom chat = new ApnaChatRoomImpl();  
      
          User1 u1=new User1(chat);  
          u1.setname("Ashwani Rajput");  
          u1.sendMsg("Hi Ashwani! how are you?");  
        
                
          User2 u2=new User2(chat);  
          u2.setname("Soono Jaiswal");  
          u2.sendMsg("I am Fine ! You tell?");  
    }  
  
}// End of the MediatorPatternDemo class.
```  

#### Output

<br>

![output](images/dp37.png)

## Memento Pattern

<br>

* A Memento Pattern says that "to restore the state of an object to its previous state". But it must do this without violating Encapsulation. Such case is useful in case of error or failure.

* The Memento pattern is also known as Token.

* Memento design pattern is used to implement the undo operation. This is done by saving the current state of the object as it changes state.

<br>

<!-- style="font-size:20px;"-->
**Advantages**
* It preserves encapsulation boundaries.
* It simplifies the originator.

<!-- style="font-size:20px;"-->
Usage

* It is used in Undo and Redo operations in most software.
* It is also used in database transactions.

### UML for Memento Pattern

<br>

![Uml](images/dp38.png)

<br>

**Memento:**
Stores internal state of the originator object. The state can include any number of state variables.
The Memento must have two interfaces, an interface to the caretaker. This interface must not allow any operations or any access to internal state stored by the memento and thus maintains the encapsulation. The other interface is Originator and it allows the Originator to access any state variables necessary to the originator to restore the previous state.

**Originator:**
Creates a memento object that will capture the internal state of Originator.
Use the memento object to restore its previous state.

**Caretaker:**
Responsible for keeping the memento.
The memento is transparent to the caretaker, and the caretaker must not operate on it.


### Example for Memento Pattern

<br>

<!-- style="font-size:20px;"-->
1. [Create an Originator class](#create-an-originator-class)

<!-- style="font-size:20px;"-->
2. [Create a Memento class](#create-a-memento-class)

<!-- style="font-size:20px;"-->
3. [Create a Caretaker class](#create-a-caretaker-class)

<!-- style="font-size:20px;"-->
4. [Create a MementoPatternDemo class](#create-a-mementopatterndemo-class)


#### Create an Originator class 

<br>

* Create an Originator class that will use Memento object to restore its previous state.

```java
//This is a class.  
  
public class Originator {  
      
       private String state;  
      
       public void setState(String state){  
          this.state = state;  
       }  
      
       public String getState(){  
          return state;  
       }  
      
       public Memento saveStateToMemento(){  
          return new Memento(state);  
       }  
      
       public void getStateFromMemento(Memento Memento){  
          state = Memento.getState();  
       }  
}// End of the Originator class. 
``` 

#### Create a Memento class

<br>

* Create a Memento class that will Store internal state of the Originator object.

```java
//This is a class.  
  
public class Memento {  
      
    private String state;  
  
    public Memento(String state) {  
        this.state=state;  
    }  
    public String getState() {  
        return state;  
    }  
      
}// End of the Memento class. 
``` 

#### Create a Caretaker class

<br>

* Create a Caretaker class that will responsible for keeping the Memento

```java
//This is a class.  
  
import java.util.ArrayList;  
import java.util.List;  
  
  
public class Caretaker {  
      
    private List<Memento> mementoList = new ArrayList<Memento>();  
  
       public void add(Memento state){  
          mementoList.add(state);  
       }  
  
       public Memento get(int index){  
          return mementoList.get(index);  
       }  
  
}// End of the Caretaker class. 
``` 

#### Create a MementoPatternDemo class

<br>

```java
public class MementoPatternDemo {  
      
    public static void main(String[] args) {  
          
          Originator originator = new Originator();  
            
          Caretaker careTaker = new Caretaker();  
            
          originator.setState("State #1");  
          careTaker.add(originator.saveStateToMemento());  
          originator.setState("State #2");  
          careTaker.add(originator.saveStateToMemento());  
          originator.setState("State #3");  
          careTaker.add(originator.saveStateToMemento());  
          originator.setState("State #4");  
  
          System.out.println("Current State: " + originator.getState());          
          originator.getStateFromMemento(careTaker.get(0));  
          System.out.println("First saved State: " + originator.getState());  
          originator.getStateFromMemento(careTaker.get(1));  
          System.out.println("Second saved State: " + originator.getState());  
          originator.getStateFromMemento(careTaker.get(2));  
          System.out.println("Third saved State: " + originator.getState());  
       }  
  
}  
// End of the MementoPatternDemo class. 
``` 

#### Output

<br>

![output](images/dp39.png)

## Observer Pattern

<br>

* An Observer Pattern says that "just define a one-to-one dependency so that when one object changes state, all its dependents are notified and updated automatically".

* The observer pattern is also known as Dependents or Publish-Subscribe.

<br>

<!-- style="font-size:20px;"-->
Advantages:

* It describes the coupling between the objects and the observer.
* It provides the support for broadcast-type communication.

<br>

<!-- style="font-size:20px;"-->
Usage:

* When the change of a state in one object must be reflected in another object without keeping the objects tight coupled.
* When the framework we writes and needs to be enhanced in future with new observers with minimal chamges.


### UML for Observer Pattern

<br>

![Uml](images/dp40.png)


### Example for Observer Pattern

<br>

<!-- style="font-size:20px;"-->
1. [Create a ResponseHandler1 class](#create-a-responsehandler1-class)

<!-- style="font-size:20px;"-->
2. [Create a ResponseHandler2 class](#create-a-responsehandler2-class)

<!-- style="font-size:20px;"-->
3. [Create an EventSource class](#create-an-eventsource-class)


#### Create a ResponseHandler1 class

<br>

* Create a ResponseHandler1 class the will implement the java.util.Observer interface.


```java
//This is a class.  
  
import java.util.Observable;  
import java.util.Observer;  
  
public class ResponseHandler1 implements Observer {  
    private String resp;  
    public void update(Observable obj, Object arg) {  
        if (arg instanceof String) {  
            resp = (String) arg;  
            System.out.println("\nReceived Response: " + resp );  
        }  
    }  
}// End of the ResponseHandler1 interface.  
```

#### Create a ResponseHandler2 class

<br>

* Create a ResponseHandler2 class the will implement the java.util.Observer interface.

```java
//This is a class.  
  
import java.util.Observable;  
import java.util.Observer;  
  
public class ResponseHandler2 implements Observer {  
    private String resp;  
    public void update(Observable obj, Object arg) {  
        if (arg instanceof String) {  
            resp = (String) arg;  
            System.out.println("\nReceived Response: " + resp );  
        }  
    }  
}// End of the ResponseHandler2 interface.
```

#### Create an EventSource class

<br>

* Create an EventSource class that will extend the java.util.Observable class .

```java
//This is a class.  
  
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStreamReader;  
import java.util.Observable;  
  
public class EventSource extends Observable implements Runnable {  
    @Override  
    public void run() {  
        try {  
            final InputStreamReader isr = new InputStreamReader(System.in);  
            final BufferedReader br = new BufferedReader(isr);  
            while (true) {  
                String response = br.readLine();  
                setChanged();  
                notifyObservers(response);  
            }  
        }  
        catch (IOException e) {  
            e.printStackTrace();  
        }  
    }  
}// End of the Eventsource class.  d of the ResponseHandler2 interface.
```


#### Output

<br>

![output](images/dp41.png)


## State Pattern

<br>

* A State Pattern says that "the class behavior changes based on its state". 
* In State Pattern, we create objects which represent various states and a context object whose behavior varies as its state object changes.

* The State Pattern is also known as Objects for States.

<br>

<!-- style="font-size:20px;"-->
Advantages:

* It keeps the state-specific behavior.
* It makes any state transitions explicit.

<!-- style="font-size:20px;"-->
Usage:

* When the behavior of object depends on its state and it must be able to change its behavior at runtime according to the new state.
* It is used when the operations have large, multipart conditional statements that depend on the state of an object.


### UML for State Pattern

<br>

![Uml](images/dp42.png)


### Example for State Pattern

<br>

<!-- style="font-size:20px;"-->
1. [Create a Connection interface ](#create-an-originator-class)

<!-- style="font-size:20px;"-->
2. [Create an Accounting class](#create-a-memento-class)

<!-- style="font-size:20px;"-->
3. [Create a Sales class](#create-a-caretaker-class)

<!-- style="font-size:20px;"-->
4. [Create a Management class](#create-a-mementopatterndemo-clas)

<!-- style="font-size:20px;"-->
5. [Create a Controller class](#create-a-caretaker-class)

<!-- style="font-size:20px;"-->
6. [Create a StatePatternDemo class](#create-a-caretaker-class)



#### Create a Connection interface

<br>

* Create a Connection interface that will provide the connection to the Controller class.

```java
//This is an interface.  
  
public interface Connection {  
  
       public void open();  
       public void close();  
       public void log();  
       public void update();  
}// End of the Connection interface.
```  

#### Create an Accounting class

<br>

* Create an Accounting class that will implement to the Connection interface.

```java
//This is a class.  
public class Accounting implements Connection {  
      
       @Override  
       public void open() {  
          System.out.println("open database for accounting");  
       }  
       @Override  
       public void close() {  
          System.out.println("close the database");  
       }  
         
       @Override  
       public void log() {  
          System.out.println("log activities");  
       }  
         
       @Override  
       public void update() {  
           System.out.println("Accounting has been updated");  
       }  
}// End of the Accounting class.
```

#### Create a Sales class

<br>

* Create a Sales class that will implement to the Connection interface.

```java
//This is a class.  
public class Sales implements Connection {  
      
      @Override  
       public void open() {  
          System.out.println("open database for sales");  
       }  
       @Override  
       public void close() {  
          System.out.println("close the database");  
       }  
         
       @Override  
       public void log() {  
          System.out.println("log activities");  
       }  
         
       @Override  
       public void update() {  
           System.out.println("Sales has been updated");  
       }  
  
}// End of the Sales class.
```  


#### Create a Management class

<br>

* Create a Management class that will implement to the Connection interface.


```java
//This is a class.  
   
public class Management implements Connection {  
      
      @Override  
       public void open() {  
          System.out.println("open database for Management");  
       }  
       @Override  
       public void close() {  
          System.out.println("close the database");  
       }  
         
       @Override  
       public void log() {  
          System.out.println("log activities");  
       }  
         
       @Override  
       public void update() {  
           System.out.println("Management has been updated");  
       }  
  
}  
 // End of the Management class.
```  

#### Create a Controller class

<br>

* Create a Controller class that will use the Connection interface for connecting with different types of connection.

```java
//This is a class.  
  
public class Controller {  
      
       public static Accounting acct;  
       public static Sales sales;  
       public static Management management;  
         
       private static Connection con;  
         
       Controller() {  
           acct = new Accounting();  
           sales = new Sales();  
           management = new Management();  
       }  
      
       public void setAccountingConnection() {  
           con = acct;  
       }  
       public void setSalesConnection() {  
           con  = sales;  
       }  
       public void setManagementConnection() {  
           con  = management;  
       }  
       public void open() {  
           con .open();  
       }  
       public void close() {  
           con .close();  
       }  
       public void log() {  
           con .log();  
       }  
       public void update() {  
           con .update();  
       }  
         
  
}// End of the Controller class. 
``` 

#### Create a StatePatternDemo class

<br>

* Create a StatePatternDemo class.

```java
//This is a class.  
  
public class StatePatternDemo {  
  
       Controller controller;  
       StatePatternDemo(String con) {  
          controller = new Controller();  
          //the following trigger should be made by the user  
          if(con.equalsIgnoreCase("management"))  
             controller.setManagementConnection();  
          if(con.equalsIgnoreCase("sales"))  
             controller.setSalesConnection();  
          if(con.equalsIgnoreCase("accounting"))  
                 controller.setAccountingConnection();  
          controller.open();  
          controller.log();  
          controller.close();  
          controller.update();  
       }  
         
         
       public static void main(String args[]) {  
  
           new StatePatternDemo(args[0]);  
             
       }  
  
}// End of the StatePatternDemo class.
```  

#### Output

<br>

![output](images/dp43.png)


## Strategy Pattern

<br>

* A Strategy Pattern says that "defines a family of functionality, encapsulate each one, and make them interchangeable".

* The Strategy Pattern is also known as Policy.

<br>

<!-- style="font-size:20px;"-->
Advantages:

* It provides a substitute to subclassing.
* It defines each behavior within its own class, eliminating the need for conditional statements.
* It makes it easier to extend and incorporate new behavior without changing the application.

<!-- style="font-size:20px;"-->
Usage:

* It is used when the multiple classes differ only in their behaviors.e.g. Servlet API.
* It is used when you need different variations of an algorithm.

<br>

![pattern](images/dp44.png)


### UML for Strategy Pattern

<br>

![Uml](images/dp45.png)


### Example for Strategy Pattern

<br>

<!-- style="font-size:20px;"-->
1. [Create a Strategy interface](#create-a-strategy-interface)

<!-- style="font-size:20px;"-->
2. [Create a Addition class](#create-a-addition-class)

<!-- style="font-size:20px;"-->
3. [Create a Subtraction class](#create-a-subtraction-class)

<!-- style="font-size:20px;"-->
4. [Create a Multiplication class](#create-a-multiplication-class)

<!-- style="font-size:20px;"-->
5. [Create a Context class](#create-a-context-class)

<!-- style="font-size:20px;"-->
6. [Create a StartegyPatternDemo class](#create-a-startegypatterndemo-class)


#### Create a Strategy interface

<br>

```java
//This is an interface.  
  
public interface Strategy {  
      
    public float calculation(float a, float b);  
  
}// End of the Strategy interface.
```  

#### Create a Addition class

<br>

* Create a Addition class that will implement Startegy interface.

```java
//This is a class.  
public class Addition implements Strategy{  
  
    @Override  
    public float calculation(float a, float b) {  
        return a+b;  
    }  
  
}// End of the Addition class. 
``` 

#### Create a Subtraction class

<br>

* Create a Subtraction class that will implement Startegy interface.

```java
//This is a class.  
public class Subtraction  implements Strategy{  
  
    @Override  
    public float calculation(float a, float b) {  
        return a-b;  
    }  
  
}// End of the Subtraction class.
```  

#### Create a Multiplication class

<br>

* Create a Multiplication class that will implement Startegy interface.

```java
//This is a class.  
  
public class Multiplication implements Strategy{  
  
    @Override  
    public float calculation(float a, float b){  
        return a*b;  
    }  
}// End of the Multiplication class. 
``` 

#### Create a Context class

<br>

* Create a Context class that will ask from Startegy interface to execute the type of strategy.

```java
//This is a class.  
  
  
public class Context {  
  
       private Strategy strategy;  
       
       public Context(Strategy strategy){  
          this.strategy = strategy;  
       }  
  
       public float executeStrategy(float num1, float num2){  
          return strategy.calculation(num1, num2);  
       }  
}// End of the Context class. 
``` 

#### Create a StartegyPatternDemo class

<br>

```java
//This is a class.  
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStreamReader;  
  
public class StrategyPatternDemo {  
      
    public static void main(String[] args) throws NumberFormatException, IOException {  
          
          BufferedReader br=new BufferedReader(new InputStreamReader(System.in));  
          System.out.print("Enter the first value: ");  
          float value1=Float.parseFloat(br.readLine());  
          System.out.print("Enter the second value: ");  
          float value2=Float.parseFloat(br.readLine());  
          Context context = new Context(new Addition());          
          System.out.println("Addition = " + context.executeStrategy(value1, value2));  
  
          context = new Context(new Subtraction());       
          System.out.println("Subtraction = " + context.executeStrategy(value1, value2));  
  
          context = new Context(new Multiplication());        
          System.out.println("Multiplication = " + context.executeStrategy(value1, value2));  
       }  
  
}// End of the StrategyPatternDemo class.
```  

## Template Pattern

<br>

* A Template Pattern says that "just define the skeleton of a function in an operation, deferring some steps to its subclasses".

<br>

<!-- style="font-size:20px;"-->
Advantages:

* It is very common technique for reusing the code.This is only the main benefit of it.

<br>

<!-- style="font-size:20px;"-->
Usage:

* It is used when the common behavior among sub-classes should be moved to a single common class by avoiding the duplication.

### UML for Template Pattern

<br>

![Uml](images/dp47.png)


### Example for Template Pattern

<br>

<!-- style="font-size:20px;"-->
1. [Create a Game abstract class](#create-a-game-abstract-class)

<!-- style="font-size:20px;"-->
2. [Create a Chess class](#create-a-chess-class)

<!-- style="font-size:20px;"-->
3. [Create a Soccer class](#create-a-soccer-class)

<!-- style="font-size:20px;"-->
4. [Create a TemplatePatternDemo class](#create-a-templatepatterndemo-class)


#### Create a Game abstract class

<br>

```java
//This is an abstract class.  
public abstract class Game {  
      
       abstract void initialize();  
       abstract void start();  
       abstract void end();  
      
       public final void play(){  
  
          //initialize the game  
          initialize();  
  
          //start game  
          start();  
            
          //end game  
          end();  
       }  
}// End of the Game abstract class. 
``` 

#### Create a Chess class

<br>

* Create a Chess class that will extend Game abstract class for giving the definition to its method.

```java
//This is a class.  
  
public class Chess extends Game {  
     @Override  
       void initialize() {  
          System.out.println("Chess Game Initialized! Start playing.");  
       }  
     @Override  
       void start() {  
          System.out.println("Game Started. Welcome to in the chess game!");  
       }  
    @Override  
       void end() {  
          System.out.println("Game Finished!");  
       }  
}// End of the Chess class.
```  

#### Create a Soccer class

<br>

* Create a Soccer class that will extend Game abstract class for giving the definition to its method.

```java
//This is a class.  
  
  
public class Soccer extends Game {  
      
    @Override  
       void initialize() {  
          System.out.println("Soccer Game Initialized! Start playing.");  
       }  
  
    @Override  
       void start() {  
          System.out.println("Game Started. Welcome to in the Soccer game!");  
       }  
         
    @Override  
       void end() {  
          System.out.println("Game Finished!");  
       }  
}// End of the Soccer class.
```

#### Create a TemplatePatternDemo class

<br>

```java
//This is a class.  
public class TemplatePatternDemo {  
  
public static void main(String[] args) throws InstantiationException, IllegalAccessException, ClassNotFoundException {  
          
         Class c=Class.forName(args[0]);  
         Game game=(Game) c.newInstance();  
         game.play();     
       }  
}// End of the Soccer class.
```  

#### Output

<br>

![output](images/dp48.png)





