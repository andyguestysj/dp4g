---
title: Model-View-Controller Pattern
permalink: /docs/pattern-1/
---

**Adapted from**  
* [GeeksForGeeks](https://www.geeksforgeeks.org/mvc-design-pattern/)  
* [tutorialspoint.com](https://www.tutorialspoint.com/design_pattern/mvc_pattern.htm)

### Model View Controller

The Model View Controller (MVC) design pattern specifies that an application consist of a data model, presentation information, and control information. The pattern requires that each of these be separated into different objects.  

MVC is more of an architectural pattern, but not for complete application. MVC mostly relates to the UI / interaction layer of an application. You’re still going to need business logic layer, maybe some service layer and data access layer.  

**UML Diagram MVC Design Pattern**  
![Model View Controller Pattern Diagram](/assets/img/pat1/MVC-Design-Pattern.png "Model View Controller pattern diagram") 

* The **Model** contains only the pure application data, it contains no logic describing how to present the data to a user.
* The **View** presents the model’s data to the user. The view knows how to access the model’s data, but it does not know what this data means or what the user can do to manipulate it.
* The **Controller** exists between the view and the model. It listens to events triggered by the view (or another external source) and executes the appropriate reaction to these events. In most cases, the reaction is to call a method on the model. Since the view and the model are connected through a notification mechanism, the result of this action is then automatically reflected in the view.

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

