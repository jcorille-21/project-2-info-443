# Project 2: Mongoose

## By Jason Xu, Crosby Huang, David Xie, Jerome Orille

# Introduction

Mongoose provides an Object Relational Model (ORM) for Node.js applications to connect to MongoDB NoSQL databases. This framework is primarily written in JavaScript with a little bit of TypeScript code.

Mongoose is an abstracted  interface of MongoDB by defining models to interact with the database using native JavaScript syntax and semantics. Users can define a schema and perform query operations on MongoDB using Mongoose. Additionally, it provides an option for users to enforce strongly-typed schemas as well. Overall the library aims to make working with MongoDB easier for JavaScript application developers with the features mentioned above.

People who maintain mongoose are a team or company called Automattic. This company also maintains a bunch of other websites or applications like Tumblr, Jetpack, and Gravatar. The Automattic company is in charge of approving changes to the code.

- The Mongoose code’s GitHub repository is [https://github.com/Automattic/mongoose](https://github.com/Automattic/mongoose)
- The Mongoose API and usage documentation is [https://mongoosejs.com/docs/guides.html](https://mongoosejs.com/docs/guides.html)
- The MongoDB query documentation is [https://docs.mongodb.com/manual/introduction/](https://docs.mongodb.com/manual/introduction/) (however, it is not necessary to write MongoDB queries in JavaScript programs that uses Mongoose)

# Development View

## Component Diagram

![Component Diagram](img/componentDiagram.png)
*Figure 1: Components of Mongoose*

We created a component diagram that details relationships between other components. Our components scope is limited to **directories/folders**. Our reasoning is that there are too many code files to individually analyze, so breaking it up into directories as components felt like the natural thing to do. In our diagram, each component has a **required interface** section and a **provided interface** section.

Required interfaces include modules that are needed for the module to work. Modules marked with a + are outside modules like `assert` or `mongodb`, while modules marked with a - are Mongoose modules.  For example, the `cast` directory requires`assert`, which is an outside dependency, and at least one file in the `driver` directory.

Provided interfaces include modules that need the module to work. Going back to the `cast` directory, the `helpers` directory needs at least one file provided from the `cast` directory for its modules to work. This is why the `helpers` directory is listed as a provided interface for the `cast` component.

Initially the components were linked together by relationship, but this ended up being very messy for a model. The components are in the /lib directory, which is the directory at the very top. The /lib directory contains all folders underneath. The folders are listed below:

|**Directory**|**Description**|
|---|---|
|`/lib`|Contains Mongoose source code and JavaScript files that start the program|
|`/cast`|Converts primitives and objects to other types|
|`/cursor`|Used for table navigation|
|`/driver`|Sets up connection information|
|`/error`|Error handling functions|
|`/helpers`|Helper functions for use in other modules|
|`/options`|Populates interface with changeable options|
|`/plugins`|Additional options users may install|
|`/schema`|Defines a MongoDB schema, which is like a table in SQL|
|`/types`|Defines objects that may be used in Mongoose|


## Source Code Structures

![Codeline Model](img/codelineModel.png)
*Figure 2: Mongoose Source Code*

Our codeline model shows **all the source code** in the Mongoose repository.  Again, we used **directories** for the codeline model because directories are more in line with the scope of Mongoose’s architecture rather than individual files. Many folders, like `/lib`, have many directories underneath them as well. This diagram is shown above. There is a table below that also describes the codeline model more thoroughly.

| Root folder | Directory Level 1 | Directory Level 2     | Feature                                                                                                                                                                                                                     |
|-------------|-------------------|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /           |                   |                       | Contains everything of the Mongoose module, including library codes, test suites, documentations, example programs, and more.                                                                                               |
|             | .github/          |                       | Github repository-specific content, showing project funding channels, issue template, and pull request templates                                                                                                            |
|             |                   | workflow/             | Contain Github workflow files, such as automate running Mocha tests in the test/ directory                                                                                                                                  |
|             | benchmarks/       |                       | Performance benchmark JavaScript programs for testing Mongoose framework’s performance (in-practice runtime).                                                                                                               |
|             | docs/             |                       | All website files (HTML, CSS, JavaScript) for Mongoose documentation site: https://mongoosejs.com/ , applicable to Mongoose 6.2.x, 5.13.x, 4.13.x versions.                                                                 |
|             |                   | 2.7.x/ to 3.5.x/      | Contains website files for documentations of old versions of Mongoose.                                                                                                                                                      |
|             |                   | all other directories | Folders that group a number of similar website dependency files together (such as pictures on this site in images/ folder and website JavaScript files located in js/ files)                                                |
|             | examples/         |                       | This directory contains sample Mongoose programs that can be run on Node.js environments. External JavaScript developers can quickly get started on using Mongoose by referencing .js codes in this directory.              |
|             |                   | all directories       | Folders that group a number of .js files showcasing different Mongoose capabilities/functions together, allowing external JS developers quickly locate sample programs by features (what goal do these programs accomplish) |
|             | lib/              |                       | The root folder of Mongoose source code.                                                                                                                                                                                    |
|             |                   | all directories       | Refer to the above table for what the source code inner folders are about.                                                                                                                                                  |
|             | test/             |                       | Unit testing files that test the Mongoose functionality and correctness. Test files are written in JavaScript using the Mocha testing framework.                                                                            |
|             |                   | all directories       | Groups a number of common test.js files based on Mongoose functionalities and components that test programs are trying to test on.                                                                                          |
|             | tools/            |                       | Contains asynchronous tools for authorization, unit testing, etc.                                                                                                                                                           |
|             | types/            |                       | Enable developers using Mongoose in TypeScript programs by providing type declarations.                                                                                                                                     |

## Testing and Configuration

Mongoose library uses Mocha testing framework to test its codes. The testing files are located underneath the `test` folder, which is located in the root folder. There are many test files that Mongoose uses.

![Test Example](img/testExample.png)
*Figure 3: Example of Testing Code*

Many test files require the use of a common test file called `common.js`. This is located underneath the `/test` folder. Some outside dependencies include the `assert` library, the `collection` component located in the `/lib` folder, and some error validation (not pictured) which is located in the `error` component in `/lib`. Since `assert` is used, this means that Mongoose utilizes **unit testing** on individual components for their testing.

![common.js](img/testExample.png)
*Figure 4: `common.js` Test File*

This `common.js` test file contains many functions that other testing files use. Figure 4 above shows the first few lines of `common.js`. Because this test file is well-defined and has common functions for use in other test files, this would be a great starting point to figure out how to test code for Mongoose.

![Testing Branches](img/differentBranches.png)
*Figure 5: Mongoose Branches*

Additionally, many developers use their own branches to test code. As of the time of fetching the repository, there are **over 100 different test branches**. Using branches allows developers to create pull requests for bug fixes and other improvements to the code. The Mongoose team would evaluate these pull requests and approve or deny changes if necessary.

# Applied Perspective

While Mongoose provides many advantages that promote its prevalence among JavaScript programs that need to interact with MongoDB, we choose to analyze Mongoose library’s **Performance Perspective**. Because Mongoose handles many queries from MongoDB, the performance of the system is very important to consider when looking at the architecture. The query speed should be fast so users perform operations on MongoDB in a timely manner.

## Response Time

When JavaScript developers uses Mongoose, they will define a typed schema by using new mongoose.Schema({}) API similar to the one below, where as each field are typed.

![](img/image10.png)
However, when JavaScript programs add data to MongoDB using Mongoose, Mongoose will first attempt to cast the provided input to the predefined schema types by going through a series of if-statement checks (which would take extra time), even though the user adds a correct-typed value. The concern of slowed response time due to type checking and casting is least useful for a large and clean dataset, according to [this blog post](https://towardsdatascience.com/the-drastic-mistake-of-using-mongoose-to-handle-your-big-data-a3c408e21a4c).

For instance, if user pass in false (a boolean-typed value) at a table field that requires boolean value, according to lib/cast/boolean.js , Mongoose still need test whether false is within `Set([true, 'true', 1, '1', 'yes'])` to see whether false is a truthy value before testing whether this falsy value. As a result, Mongoose will have a higher response time to input a false value to the database compared to input a true value.

Code snippet within `lib/cast/boolean.js file`
![](img/image15.png)

As another example, when users wants to insert a value to a String-typed field, Mongoose needs to first check whether the user passed in a null value or the user passed in the ID value of a document first, before checking whether this value can be casted to a String using the default .toString() method on an object. As a result, inserting an Object ID to a String-typed field takes less time (aka. reducing the database operations’ response time) compared to inserting a String-typed value to String-typed field; this issue is evident when we are inserting a large amount of data that is guaranteed to be String-typed.

Code snippet in `lib/cast/string.js`
![](img/image11.png)

Side note on type casting and system predictability: the time consumption of type-casting processes is predictable, as all input values always go through <type>.js file to attempt casting value to the desired type (according to the type of schema). In addition, <type>.js files’ behaviors will not change during runtime, making type-casting operation stable (even though it reduces response time for Mongoose to insert values to MongoDB.

## Throughput

MongoDB is a document-based database, indicating its data can be unstructured. If information (and its data type) within a database cannot be relied upon due to a lack of schema consistency, then it is more challenging for JavaScript client developers  to interact with MongoDB databases even via Mongoose.

When using Mongoose, JavaScript client developers can set the database schema type while defining the table schema (such as declaring a String-typed column called `title`, in the below example). In contrast, developers need to explicitly define a typed-schema separately if they use native MongoDB syntax ([source](https://docs.mongodb.com/manual/core/schema-validation/#std-label-schema-validation-json)). Thus, the schema type enforcement reduces the client code’s need to add more code to check returned data (from database) and cast to client’s desired type.

![Schema Example](img/schemaExample.png)
*Figure ???: Example of a Schema*

This allows for correctness of the data type that users receive from queries. However, as a result of having many cast checks, these checks cause a drop in performance as a result. Someone had an example of a [benchmark performance between MongoDB and Mongoose](https://bugwheels94.medium.com/performance-difference-in-mongoose-vs-mongodb-60be831c69ad), and found that MongoDB can be faster at times. This may be due to the architecture of Mongoose, where it calls from multiple sources like in `lib/cast` to `lib/modules`, etc. This would [spell trouble for larger datasets](https://towardsdatascience.com/the-drastic-mistake-of-using-mongoose-to-handle-your-big-data-a3c408e21a4c) because of the reliance on multiple modules at once. Mongoose would certainly take a performance hit with large data.

## Applying the Perspective

### Performance Model
- User executes a query
- Query goes through a cast file for processing
- Cast file performs schema type checking and validation
- Cast file then returns requested data if the query was a find operation
- Otherwise, save data into database

![Performance Model](img/performance_model.png)
*Figure ?: Benchmark Data referenced from (https://bit.ly/37whz7l) and (https://bit.ly/3MJlxK1)*

### Identify the Performance-Critical Structure
In the diagram above, the performance-critical components start at the **model** query where depending on the user’s request (reading or writing to data), it can impact the performance for the rest of the process flow. Latency is further introduced by the **casting processor** which takes in the user input data and checks if it can be casted to the enforced types in the **Data Schema**. Finally, the save() operation is executed where the row is added to the **MongoDB database** collection.

### Identify the Key Performance Metrics
In the context of Mongoose, the key metrics to evaluate were reads/writes per second and the latency time. These metrics are the most important as read and write operations are the main ones that users perform with the system. For the benchmark, the Apache Benchmark suite was used where it would fire 150 requests per second from 4 concurrent users which would be a sufficient amount to see the extent of Mongoose’s throughput limit. From the benchmark it was found that Mongoose’s throughput was 583 reads/sec and 384 writes/sec. Its latency time was 1.71ms for reads and 2.60ms for writes. It should be noted that compared to the Native MongoDB driver, its performance was significantly better with a throughput of 1200 reads/sec with 0.83ms latency and 1128 writes/sec with 0.89ms latency. This is not surprising due to the validation and type-casting processing that Mongoose needs to perform between reading or writing the given data. The latency performance loss can be significant though as one benchmark used a schema with over 750 types to validate. It was found to take around 22-30 seconds to finally save it into the database. However, disabling validation reduced the entire operation to less than 1 second. Overall, Mongoose represents a tradeoff between performance and functionality. When using Mongoose, the developer will expect degraded performance but can then obtain more features such as data validation, sanitization from possible injection attacks, and consistency within an enforced schema.

# Identify Styles and Patterns

## High-level architectural style
We believe that the mongoose applies the Layered architectural style. The users’ script works as the presentational layer and the mongoose works as the business layer, and the mongoDB is the data layer.
![Example of Layered architectural style](img/exampleOfLayered.png)

## Facade Pattern
The Mongoose itself follows an Facade pattern, as it translates between objects in JavaScript code and the representation of those objects in MongoDB. JavaScript developers can perform MongoDB operations by invoking Mongoose in typical JavaScript-like syntax rather than referencing MongoDB Shell syntax.
![Example of relationship of Mongoose and MongoDB](img/example.png)

## Decorator Pattern
Decorator Pattern
By default, Mongoose will call create “automatically calls createIndex for each defined index in your schema” when connecting users’ apps to the MongoDB database. Users can optionally pass { autoIndex: false } as the second parameter on mongoose.connect(...) to disable this default behavior. Since this object alters Mongoose’s default behavior, Mongoose’s provided interface adheres to the decorator pattern.

Create a regular MongoDB connection:
`mongoose.connect('mongodb://user:pass@localhost:port/database');`

Create a MongoDB connection without having Mongoose call createIndex:
`mongoose.connect('mongodb://user:pass@localhost:port/database', { autoIndex: false });
// or
mongoose.createConnection('mongodb://user:pass@localhost:port/database', { autoIndex: false });`

Link: [https://mongoosejs.com/docs/guide.html](https://mongoosejs.com/docs/guide.html)

##Iterator Pattern
Within lib/cursor, QueryCursor.js exposes JavaScript’s Streams3 interface, allowing client programs to call .next() function to conditionally (or in batch) advance to the next row/document of MongoDB’s table/collection. Since client programs can utilize cursor interface to access content in MongoDB (a collection of objects) without any need to know Mongoose’s underlying implementation of cursor, Mongoose’s cursor interface is an example of Iterator pattern.

[Cursor interface’s API documentation](https://mongoosejs.com/docs/api/query.html#query_Query-cursor)
![](img/image21.png)

Code snippet in `lib/cursor/QueryCursor.js`
![](img/image34.png)
And the function handling finding next element in the Collection
![](img/image30.png)

## Mediator Pattern
According to [documentation](https://mongoosejs.com/docs/tutorials/query_casting.html), when Mongoose fails to cast the passed in data type to the enforced data type in the schema, it throws an instance of the `CastError` class. Rather than handling the error processing themselves, the `castString` and `castBoolean` functions pass in the type, value, and path to the CastError class which serves as the mediator between the components. The CastError class then takes in the passed arguments and eventually returns the respective error message to be displayed back to the client. Therefore, this communication between different components (lib/cast/string.js and lib/cast/boolean.js) and the central authority, `CastError` class showcases the Mediator Pattern.

![Instance of CastError in "lib/cast/string.js"](img/CastErrorInstance.png)
*Instance of CastError in "lib/cast/string.js"*

![CastError class in “/lib/error/cast.js”](img/CastError.png)
*CastError class in "lib/error/cast.js"*

# Architectural Assessment

## Open Close Principle

### a: files/modules in `lib/schema` folder
![Open Closed Principle 1](img/OpenClosed-1.png)

Instead of hard-coding data types of Mongoose schemas, Mongoose developers opted for processing each (supported) data type in separate files/modules. They are being referenced in SchemaType(path, options, instance) located in `./lib/schematype.js` . This allows MongoDB developers to create more files/modules to support new data types of MongoDB in the future.

![Open Closed Principle 1](img/OpenClosed-2.png)

### b: `./lib/error` directory,
There are several error handling files that extend the `MongooseError` class , and the `MongooseError` class also extends the built-in JavaScript `Error` class. As a result, client classes (within Mongoose source code) can either use the `MongooseError` itself, or a more specific Error class that adds more behaviors to the `MongooseError` class, which is explained below.
![](img/image35.png)

Example 1: `lib/error/divergentArray.js`
![](img/image12.png)

In the DivergentArrayError that extends MongooseError, it has a super(msg) function that calls functions within MongooseError. This coding style follows an open-closed principle as DivergentArrayError extends MongooseError instead of modifying MongooseError behaviors.

Example 2: `lib/error/cast.js`
![](img/image9.png)
Like DivergentArrayError, CastError also extends MongooseError functionality by adding CastError’s specific behaviors, instead of modifying MongooseError behaviors.

### c: lib/cast/boolean.js
![](img/image27.png)
In the boolean.js file, one can modify which values should be interpreted as true or false by modifying content in two Set objects, without the need to modify the actual boolean casting logic. As a result, one may choose to add the equivalent of “true” or “false” in other languages (such as “oui” or “non” in French) by adding them in the convertToTrue and convertToFalse Sets.

## Single Responsibility Principle
### a: `lib/schema` folder
![Open Closed Principle 1](img/OpenClosed-1.png)

JavaScript files within `./lib/schema` handles data type (of the corresponding MongoDB schema types) individually (each JavaScript file handles own MongoDB data type). For instance, code handling String data type don’t need to know the code handling Date data type. Clients of Mongoose will define MongoDB schemas in a fashion similar to this:
`const postSchema = new mongoose.Schema({
url: String,
description: String,
username: String,
likes: [String],
created_date: Date
})`

### b: `lib/error/mongooseError.js` and Error classes (within the lib/error folder) that extend MongooseError.
![](img/image35.png)
MongooseError’s sole responsibility is to throw an Error (built-in JavaScript Error) object with the name of “Mongoose”, allowing client program developers to easily distinguish error from Mongoose or other external modules (dependencies) when debugging their JavaScript programs.

## Dependency Inversion Principle

TODO: Crosby add this part

Within `./lib/error` directory, there are several error handling files that extends `MongooseError` class , and `MongooseError` class also extends the built-in JavaScript `Error` class.
![Dependency Inversion Principle 1](img/DepInv-1.png)

![Dependency Inversion Principle 2](img/DepInv-2.png)

In the `DivergentArrayError` that extends `MongooseError`, it has a `super(msg)` function that calls the `MongooseError` super class. This coding style follows dependency inversion principle, because developers can add new (more specific) `MongooseError` class files that extends `MongooseError`.

## Principle of Least Knowledge (Law of Demeter)  (from INFO 443 OOP Principles lecture)

### a: Mongoose Schema object creation
Mongoose provides an abstracted interface allowing JavaScript programs to interact with MongoDB (such as create a table and define a schema on this table) using Mongoose syntax instead of the MongoDB native syntax. Thus, clients don’t need to understand the internals of MongoDB syntax, as long as they can use Mongoose syntax correctly. Since Mongoose translates and forwards client requests to MongoDB, Mongoose’s provided interface adheres to the Law of Demeter principle.

![Law of Demeter 1](img/Demeter-1.png)

Here is an example of [database schema creation](https://mongoosejs.com/docs/guide.html) using Mongoose syntax
![](img/Screen Shot 2022-03-14 at 4.39.56 PM.png)

The MongoDB native syntax to create a table and [define a schema](https://docs.mongodb.com/manual/core/schema-validation/#std-label-schema-validation-json) for this table is similar to this:
![](img/Screen Shot 2022-03-14 at 4.41.08 PM.png)

In contrast, for JavaScript clients using mysql and mysql2 modules to interact with MySQL database, JavaScript clients need to use SQL query to perform database operations (highlighted part are SQL syntax, the rest of them are JavaScript syntax).
![app.get](img/Screen Shot 2022-03-14 at 4.42.43 PM.png)

## b: `lib/error/mongooseError.js` and Error classes (within the `lib/error` folder) that extend `MongooseError`.

![Law of Demeter 2](img/Demeter-2.png)

Error-handling classes – such as CastError, DivergentArrayError, MissingSchemaError, DocumentNotFoundError – all extend the MongooseError object, and MongooseError extends the built-in JavaScript Error object. String, Boolean, and some other client classes interact with direct implementations of MongooseError rather than MongooseError itself, and these client classes do not need to know the behavior of MongooseError nor the built-in JavaScript Error Object. As a result, error-handling classes structures within Mongoose follow the Law of Demeter as well.

## Liskov Substitution Principle

### a: `lib/types/subdocument.js` that adds more behaviors to `lib/document.js`

For the **Liskov Substitution Principle**, there are two classes that promote this design pattern. These files are located in `lib/document.js`, which is the Document class, and `lib/types/subdocument.js`, which is the SubDocument class. See Figures ? and ?? below.

![document.js](img/documentDotJs.png)
*Figure ?: `lib/document.js`*

![subdocument.js](img/subdocumentDotJs.png)
*Figure ??: `lib/types/subdocument.js`*

These two classes promote the *Liskov Substitution Principle* because the `SubDocument` could completely replace an instance of the `Document` class. This is because the `SubDocument` checks if there is a valid parent of itself. If there isn’t, then it just calls the `Document` class. This means that the `SubDocument` instance would just be a `Document` object. There is some extra logic when it does have a parent, but it still calls the `Document` class in the end.

## b: checkRequired functions in several `.js` files within `lib/schema`, and checkRequired function of lib/schematype.js

TODO: Crosby need to add this part

## Composite Reuse Principle

### a: `lib/cast/boolean.js`

![Composite Reuse Principle 1](img/CompReuse-1.png)

Within the `./lib/cast` folder, boolean.js uses an instance of `CastError` (`throw new CastError('boolean', value, path);` ) when it can’t convert a given value to a boolean value. Since `boolean.js` does not inherit the `CastError` itself and the `CastError` can exist by itself without `boolean.js` codes, `boolean.js` follows the Composite Reuse Principle.

### b: `lib/cast/string.js`

![](img/image8.png)
Within the `./lib/cast` folder, string.js also uses an instance of CastError (throw new CastError('string', value, path); ) when it can’t convert a given value to a String value. This error throwing behavior in string.js is similar to boolean.js .

### c: `lib/schema.js`

![](img/image25.png)

Mongoose provides a `Schema.pick()` function allowing clients to “pick” a subset of schemas from the original schema. Mongoose will throw an instance of MongooseError object if the user does not pass an array in or the user's input is not in the original schema. Since this function does not inherit MongooseError but rather uses an instance of MongooseError, the `Schema.pick()` function favors composition over inheritance.