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
Mongoose applies the Pipes and the **Filters architectural style**, where the flow of data is driven by data and the whole system is decomposed into components of data source, filters, pipes, and data sinks . The users’ query will select the input  and Mongoose works as the filter, and the mongoDB is the result being fetch. 
![Example of Layered architectural style](img/exampleOfLayered.png)

## Facade Pattern
The Mongoose itself follows an Facade pattern, as it translates between objects in JavaScript code and the representation of those objects in MongoDB. JavaScript developers can perform MongoDB operations by invoking Mongoose in typical JavaScript-like syntax rather than referencing MongoDB Shell syntax.
![Example of relationship of Mongoose and MongoDB](img/example.png)



# Architectural Assessment

## Open Close Principle

![Open Closed Principle 1](img/OpenClosed-1.png)

Instead of hard coding data types of Mongoose schemas, Mongoose developers opted for processing each (supported) data types in separate files/modules. They are being referenced in SchemaType(path, options, instance) located in ./lib/schematype.js . This allows MongoDB developers to create more files/modules to support new data type of MongoDB in future.

![Open Closed Principle 1](img/OpenClosed-2.png)

## Single Responsibility Principle

![Open Closed Principle 1](img/OpenClosed-1.png)

JavaScript files within `./lib/schema` handles data type (of the corresponding MongoDB schema types) individually (each JavaScript file handles own MongoDB data type). For instance, code handling String data type don’t need to know the code handling Date data type. Clients of Mongoose will define MongoDB schemas in a fashion similar to this:
`const postSchema = new mongoose.Schema({
url: String,
description: String,
username: String,
likes: [String],
created_date: Date
})`

## Dependency Inversion Principle

a: `.lib/cast.js`
![Dependency Inversion Principle 2](img/exampleOfDependcy.png)
Within `.lib/cast.js`, the function `_cast(val, numbertype, context)` assigns `numbertype.castForQuery({ val: item, context: context })` function to val[nkey] . However, depending on the content of numbertype, the client who invoke `castForQuery()` method will conditionally invoke different implementations of `castForQuery()` based on the schema data type (such as `castForQuery()` of `.lib/schema/date.js` or `.lib/schema/boolean.js`). Hence cast.js doesn't need to consider which implementation of `castForQuery()` should cast.js call as long as cast.js knows the data type of value that needs to be casted. Thus cast.js adheres to the dependency inversion principle.


## Interface Segregation Principle
TODO

##Law of Demeter

Web applications using Mongoose will communicate with Mongoose itself, rather directly to MongoDB. Mongoose forward clients’ requests to MongoDB.

![Law of Demeter 1](img/Demeter-1.png)

Also, the example used in Open Close Principle and Single Responsibility Principle follows the Law of Demeter, as the function using a Data Type processor (with respect to MongoDB Data Type) don’t need to know the actual implementation of processors themselves.

## Liskov Substitution Principle
b: checkRequired functions in several .js files within `.lib/schema`, and checkRequired function of `.lib/schematype.js`
checkRequired function in `.lib/schematype.js`

![checkRequired function in lib/schematype.js](img/Liskov-Substitution.png)

Within the `.lib/schema/operators` folder, boolean.js and number.js all use the same  checkRequired function in lib/schematype.js. Thus this match the *Liskov Substitution Principle* because these “SubDocuments” replace and override the instance from the schematype class. For example, in number.js, it overrides the function the required validator uses to check whether a **string value** passes the ‘required’ check. While in boolean.js, they override the function the required validator uses to check whether a **boolean value** passes the ‘required’ check.

![Code of lib/schema/boolean.js](img/Liskov-Substitution.png)
![Code of lib/schema/boolean.js](img/Liskov-Substitution1.png)
![Code of lib/schema/number.js](img/Liskov-Substitution2.png)

## Composite Reuse Principle



Within `./lib/cast` folder, `boolean.js` uses an instance of `CastError` when it can’t convert a given to a boolean value. Since `boolean.js` does not inherit the `CastError` itself and the `CastError` can exist by itself without `boolean.js` codes, `boolean.js` follows the Composite Reuse Principle.
