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
* Visitor Pattern


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

<!-- style="font-size:20px"-->
**Step 1 :** Create a Plan abstract class.

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

<br>

<!-- style="font-size:20px"-->
**Step 2 :** Create the concrete classes that extends Plan abstract class.

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

<br>

<!-- style="font-size:20px"-->
**Step 3 :** Create a GetPlanFactory to generate object of concrete classes based on given information..

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

<!-- style="font-size:20px"-->
**Step 4 :** Generate Bill by using the GetPlanFactory to get the object of concrete classes by passing an information such as type of plan DOMESTICPLAN or COMMERCIALPLAN or INSTITUTIONALPLAN.

<br>

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
**OUTPUT :**

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

Here, we are calculating the loan payment for different banks like **HDFC, ICICI, SBI** etc.

<br>

<!-- style="font-size:20px"-->
**Step 1 :** Create a Bank interface

<br>

```java
import java.io.*;     
interface Bank{  
        String getBankName();  
}  
```

<br>

<!-- style="font-size:20px"-->
**Step 2 :** Create concrete classes that implement the Bank interface.

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

<br>

<!-- style="font-size:20px"-->
**Step 3 :** Create the Loan abstract class.

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

<br>

<!-- style="font-size:20px"-->
**Step 4 :** Create concrete classes that extend the Loan abstract class..

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

<br>

<!-- style="font-size:20px"-->
**Step 5 :** Create an abstract class (i.e AbstractFactory) to get the factories for Bank and Loan Objects.

<br>

```java
abstract class AbstractFactory{  
  public abstract Bank getBank(String bank);  
  public abstract Loan getLoan(String loan);  
}
```  

<br>

<!-- style="font-size:20px"-->
**Step 6 :** Create the factory classes that inherit AbstractFactory class to generate the object of concrete class based on given information.

<br>

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

<!-- style="font-size:20px"-->
**Step 7 :** Create a FactoryCreator class to get the factories by passing an information such as Bank or Loan.

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

<br>

<!-- style="font-size:20px"-->
**Step 8 :** Use the FactoryCreator to get AbstractFactory in order to get factories of concrete classes by passing an information such as type.

<br>

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
**OUTPUT :**

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

https://github.com/dharmananda4444/Design-Patterns/blob/version-1.0/README.md


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


