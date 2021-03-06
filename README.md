easydao-project
===============

EasyDao is a lightweight, fast and flexible model and dao code generator.

# What is EasyDao? 

* no JPA
* no Hibernate
* no heavyweight tools
* no special knowledge
* no cost
* supports new and old projects
* generates model as POJO
* generates Dao for Spring Framework JdbcTemplate
* CRUD Dao methods
* ultra lightweight dependency
* you get meta information about database (metadata.txt)
* based on maven
* configuration is very simple
* configuration in pom.xml
* open source and free with MIT licence
* ultra fast code generation
* you can use it from Jenkins
* handling composite primary keys
* handling arrays
* handling primary key sequences
* database design is convention over configuration
* flexible: replace the table and field names without changing database
* open source and free demo application
* learning time is about 5 minutes

**EasyDao has tested on Oracle 10, 11 and PostgreSQL 9. Maybe it works with other Oracle and PostgreSQL versions.**

> If you want to use it, then you need **easydao-maven-plugin** and **easydao-core**. You can see how to use it with demo applications: easydao-demo and easydao-demo-database-model. More information on GitHub page.

Check it out:

https://github.com/vanioinformatika/easydao-maven-plugin

https://github.com/vanioinformatika/easydao-core

https://github.com/vanioinformatika/easydao-demo

https://github.com/vanioinformatika/easydao-demo-database-model

If you want all sources or you are a developer of EasyDao, then clone the following repositories:

1. **easydao:** engine of easydao. It is generating source code from database. Runnable project for integration testing.
1. **easydao-core:** dependency all java source code that was generated by easydao.
1. **easydao-maven-plugin:** maven plugin for easydao, depends on _easydao._
1. **easydao-demo-database-model:** An example maven project for using easydao maven plugin in your project.
1. **easydao-demo:** An example application for using generated model classes.
1. and **easydao-project** (this one).

If you are using NetBeans, then **open easydao-project.** 

# EasyDao logic

> This section describes EasyDao logic. This means how to create your projects and database, and what conventions are.

There are four logic layer:

## Database

This is your real database. It is important that table and field names are following naming conventions, e.g: if you prefixes tables (CUS_CUSTOMER), than all table must have prefix. EasyDao has a feature for replacing wrong table and/or field names. See: https://github.com/vanioinformatika/easydao-maven-plugin#replacementtablefilename

Tables must have at least one primary key. **I advice that, do not use composite primary keys, but always use at least one primary key.** See: http://stackoverflow.com/questions/1383062/composite-primary-key


## Dao and Model layer

These classes generated from the database, and you never modify it manually. Dao classes directly reaches tables of database. The dao classes based on Spring Framework JdbcTemplate.

## DaoExt and DaoComp layer

They provides the necessary business logic on database. Not autogenerated classes. EasyDao gives interfaces for it.

DaoExt classes extends Dao classes, and contains several unique methods **for exactly one table.** DaoComp classes not related to one table. They are **using several tables with one complex query.**

DaoExt classes must implements hu.vanio.easydao.core.DaoExt interface. DaoComp classes must implements hu.vanio.easydao.core.DaoComp interface.

## Service layer

Service classes contains Spring @Transactional annotation, and they are using Dao, DaoExt and DaoComp classes. Services implements business logic, collaboration between database, queue, filesystem, algorithm, etc. Not autogenerated classes. **Service layer never contains SQL codes!** It is using Dao classes: Dao, DaoExt and DaoComp.

**DaoExt, DaoComp and Service classes are depends on business logic and created by developers.** 

You can see this one on the next image and PDF. 

Download as PDF:
[EasyDao logic](../master/easydao-logic.pdf)
![easydao-logic](../master/easydao-logic.png "EasyDao Logic")

Download as PDF:
[EasyDao logic](../master/easydao-workflow.pdf)
![easydao-workflow](../master/easydao-workflow.png "EasyDao Workflow")



