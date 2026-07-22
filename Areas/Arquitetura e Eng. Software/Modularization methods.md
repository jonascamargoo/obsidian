---
tipo: conceito
area: Arquitetura e Eng. Software
tags:
- dev/arquitetura
criada: '2024-10-14'
---

### What is modularization? 

Modularization is the process of decoupling a software system into multiple modules. In addition to reducing complexity, it increases the understandability, maintainability and reusability of the system.

### Package by Layer vs Package by Feature

###### Package by Layer

In this project structure, classes are placed in the architectural layer package they belong to. This method causes low Cohesion -  [[Coupling X Cohesion]]  within packages because packages contain classes that are not closely related to each other. Below is an example of packaging by layers:

├── com.app  
	└── controller  
		├── CompanyController  
		├── ProductController  
		└── UserController  
	└── model  
		├── Company  
		├── Product  
		└── User  
	└── repository  
		├── CompanyRepository  
		├── ProductRepository  
		└── UserRepository  
	└── service  
		├── CompanyService  
		├── ProductService  
		└── UserService  
	└── util

When we examine this structure, we see that there will be high coupling between packages as well as low cohesion within packages. Since `Repository` classes will be used in `Service` classes and `Service` classes will be used in `Controller` classes, high coupling occurs between packages. Moreover, it is necessary to make changes in many packages to implement the requirements.

`“I felt like I had to understand everything in order to help with anything.” — Sandi Metz`


###### Package by Feature

In this project structure, packages contain all classes that are required for a feature. The independence of the package is ensured by placing closely related classes in the same package. An example of this structure is given below:

├── com.app  
	└── company  
		├── Company  
		├── CompanyController  
		├── CompanyRepository  
		└── CompanyService  
	└── product  
		├── Product  
		├── ProductController  
		├── ProductRepository  
		└── ProductService  
	└── util  
	└── user  
		├── User  
		├── UserController  
		├── UserRepository  
		└── UserService
The use of a class by a class in another package is eliminated with this structure. Also, the classes within the packages are closely related to each other. Thus, there is **high cohesion within packages** and **low coupling between packages.** In addition, this structure provides higher modularity. How? Let’s assume there are 10 more domains, not just Company, Product and User. In the Package by Layer, Controllers, Services, and Repositories are placed in different single packages, so the whole application consists of three packages — except util — and packages have a large number of members. However, in the Package by Feature style, the same application consists of 13 packages and thus, modularity is increased.


## **Advantages of Package by Feature**

— As mentioned, Package by Feature has packages with **high cohesion, low coupling** and **high modularity.**

— Package by Feature allows some classes to set their access modifier `package-private` instead of `public`, so it increases **encapsulation**. On the other hand, Package by Layer forces you to set nearly all classes `public`.

— Package by Feature reduces the need to navigate between packages since all classes needed for a feature are in the same package.

— Package by Feature is like microservice architecture. Each package is limited to classes related to a particular feature. On the other hand, Package By Layer is monolithic. As an application grows in size, the number of classes in each package will increase without bound. Easier to migrate.


