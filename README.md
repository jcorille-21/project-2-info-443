# Project 2: Mongoose

## By Jason Xu, Crosby Huang, David Xie, Jerome Orille

# Introduction

Mongoose provides an Object Relational Model (ORM) for Node.js applications to connect to MongoDB NoSQL databases. This framework is primarily written in JavaScript with a little bit of TypeScript code.

Mongoose is used as an interface to MongoDB by defining models to interact with the database. Some interactions that users can do include querying and any other SQL commands. This makes it necessary for users to use to access a MongoDB database. Additionally, it also enforces strongly-typed schemas as well. Overall the library aims to make working with MongoDB easier for developers with the features mentioned above.

People who maintain mongoose are a team or company called Automattic. This company also maintains a bunch of other websites or applications like Tumblr, Jetpack, and Gravatar. The Automattic company is in charge of approving changes to the code.

# Development View

![Component Diagram](img/proj2_components.png)
*Figure 1: Components of Mongoose*

We created a component diagram that details relationships between other components. Our components scope is limited to **directories/folders**. Our reasoning is that there are too many code files to individually analyze, so breaking it up into directories as components felt like the natural thing to do. In our diagram, each component has a **required interface** section and a **provided interface** section.

Required interfaces include modules that are needed for the module to work. Modules marked with a + are outside modules like `assert` or `mongodb`, while modules marked with a - are Mongoose modules.  For example, the `cast` directory requires`assert`, which is an outside dependency, and at least one file in the `driver` directory.

Provided interfaces include modules that need the module to work. Going back to the `cast` directory, the `helpers` directory needs at least one file provided from the `cast` directory for its modules to work. This is why the `helpers` directory is listed as a provided interface for the `cast` component.

Initially the components were linked together by relationship, but this ended up being very messy for a model. The components are in the /lib directory, which is the directory at the very top. The /lib directory contains all folders underneath. The folders are listed below:

|**Directory**|**Description**|
|---|---|
|`/cast`|Converts primitives and objects to other types|
|`/cursor`|Used for navigation|
|`/driver`|Sets up connection information|
|`/error`|Error handling functions|
|`/helpers`|Helper functions for use in other modules|
|`/options`|Populates interface with changeable options|
|`/plugins`|Additional options users may install|
|`/schema`|Defines a MongoDB schema, which is like a table in SQL|
|`/types`|Defines objects that may be used in Mongoose|

# Applied Perspective

![Schema Example](img/schema.png)
*Figure 2: Example of defined schema using Mongoose*

It’s important to understand that MongoDB is a document-based database. In contrast to relational databases, this means that their data stored can be ‘unstructured’. While this offers benefits such as a more streamlined process of updating entries in the database, the lack of a rigid schema can make it difficult to enforce restrictions or specific data types allowed to be entered in the database.

Therefore, the main perspective that the Mongoose library falls under is the **Usability Perspective** by which it allows its users (Node.js developers) to more easily interact with the target system (MongoDB database) in order to work more effectively.  As it is an Object Document Mapper (ODM), it provides the functionality for its users to actually enforce that schema design. This then serves as an interface to the MongoDB database where those users can perform CRUD operations on entries in the collection while still abiding by said schema restrictions.

With the Usability Perspective in mind, one of the main concerns that Mongoose tries to address is **Information Quality**. The concern is that if information within a database cannot be relied upon due to a lack of consistency, then the database cannot be utilized in a way that the developers intended for. Overall, the goal of this perspective in the Mongoose system is to allow developers to avoid the common pitfall of using inconsistent approaches to data entry validation when reading and writing to their databases.

# Identify Styles and Patterns

## High-level architectural style
We believe that the mongoose applies the Layered architectural style. The users’ script works as the presentational layer and the mongoose works as the business layer, and the mongoDB is the data layer.
![Example of Layered architectural style](img/exampleOfLayered.png)

## Facade Pattern
The Mongoose itself follows an Facade pattern, as it translates between objects in JavaScript code and the representation of those objects in MongoDB. JavaScript developers can perform MongoDB operations by invoking Mongoose in typical JavaScript-like syntax rather than referencing MongoDB Shell syntax.
![Example of relationship of Mongoose and MongoDB](img/example.png)



