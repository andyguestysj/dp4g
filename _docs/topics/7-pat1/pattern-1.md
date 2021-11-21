---
title: Model-View-Controller Pattern
permalink: /docs/pattern-1/
---

### Model View Controller

Model–view–controller (MVC) is a software design pattern commonly used for developing user interfaces that divide the related program logic into three interconnected elements. This is done to separate internal representations of information from the ways information is presented to and accepted from the user.  

Traditionally used for desktop graphical user interfaces (GUIs), this pattern became popular for designing web applications. Popular programming languages have MVC frameworks that facilitate implementation of the pattern.  

The Model View Controller design pattern specifies that an application consist of a data model, presentation information, and control information. The pattern requires that each of these be separated into different objects.   

MVC is more of an architectural pattern, but not for complete application. MVC mostly relates to the UI / interaction layer of an application. You’re still going to need business logic layer, maybe some service layer and data access layer.  

**UML Diagram MVC Design Pattern**  
![Model View Controller Pattern Diagram](/assets/img/pat1/MVC-Design-Pattern.png "Model View Controller pattern diagram") 

* **Model** The central component of the pattern. It is the application's dynamic data structure, independent of the user interface. It directly manages the data, logic and rules of the application.
* **View** Any representation of information such as a chart, diagram or table. Multiple views of the same information are possible, such as a bar chart for management and a tabular view for accountants.
* **Controller** Accepts input and converts it to commands for the model or view.

In addition to dividing the application into these components, the model–view–controller design defines the interactions between them.  

* The model is responsible for managing the data of the application. It receives user input from the controller.
* The view renders presentation of the model in a particular format.
* The controller responds to the user input and performs interactions on the data model objects. The controller receives the input, optionally validates it and then passes the input to the model.

#### Implementation

We are going to create a *Student* object acting as a model. *StudentView* will be a view class which can print student details on console and *StudentController* is the controller class responsible to store data in Student object and update view StudentView accordingly.  

*MVCPatternDemo*, our demo class, will use *StudentController* to demonstrate use of MVC pattern.  

**UML Diagram MVC Design Pattern**  
![Model View Controller Class Diagram](/assets/img/pat1/mvc_pattern_uml_diagram.jpg "Model View Controller Class Diagram") 

#### Code

```java
class Student
{
	private String rollNo;
	private String name;
	
	public String getRollNo()
	{
		return rollNo;
	}
	
	public void setRollNo(String rollNo)
	{
		this.rollNo = rollNo;
	}
	
	public String getName()
	{
		return name;
	}
	
	public void setName(String name)
	{
		this.name = name;
	}
}

class StudentView
{
	public void printStudentDetails(String studentName, String studentRollNo)
	{
		System.out.println("Student: ");
		System.out.println("Name: " + studentName);
		System.out.println("Roll No: " + studentRollNo);
	}
}

class StudentController
{
	private Student model;
	private StudentView view;

	public StudentController(Student model, StudentView view)
	{
		this.model = model;
		this.view = view;
	}

	public void setStudentName(String name)
	{
		model.setName(name);		
	}

	public String getStudentName()
	{
		return model.getName();		
	}

	public void setStudentRollNo(String rollNo)
	{
		model.setRollNo(rollNo);		
	}

	public String getStudentRollNo()
	{
		return model.getRollNo();		
	}

	public void updateView()
	{				
		view.printStudentDetails(model.getName(), model.getRollNo());
	}	
}

class MVCPatternDemo
{
	public static void main(String[] args)
	{
		Student model = retriveStudentFromDatabase();

		StudentView view = new StudentView();

		StudentController controller = new StudentController(model, view);

		controller.updateView();

		controller.setStudentName("Vikram Sharma");

		controller.updateView();
	}

	private static Student retriveStudentFromDatabase()
	{
		Student student = new Student();
		student.setName("Lokesh Sharma");
		student.setRollNo("15UCS157");
		return student;
	}
	
}
```

#### Advantages
* Multiple developers can work simultaneously on the model, controller and views.
* MVC enables logical grouping of related actions on a controller together. The views for a specific model are also grouped together.
* Models can have multiple views.

#### Disadvantages
* The framework navigation can be complex because it introduces new layers of abstraction and requires users to adapt to the decomposition criteria of MVC.
* Knowledge on multiple technologies becomes the norm. Developers using MVC need to be skilled in multiple technologies.



**Collated from**  
* [GeeksForGeeks](https://www.geeksforgeeks.org/mvc-design-pattern/)  
* [tutorialspoint.com](https://www.tutorialspoint.com/design_pattern/mvc_pattern.htm)
* [Wikipedia](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)