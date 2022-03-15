# Project 2: Mongoose

## By Jason Xu, Crosby Huang, David Xie, Jerome Orille

# Introduction

Mongoose provides an Object Relational Model (ORM) for Node.js applications to connect to MongoDB NoSQL databases. This framework is primarily written in JavaScript with a little bit of TypeScript code.

Mongoose is an abstracted interface of MongoDB by defining models to interact with the database using native JavaScript syntax and semantics. Users can define a schema and perform query operations on MongoDB using Mongoose. Additionally, it provides an option for users to enforce strongly-typed schemas as well. Overall the library aims to make working with MongoDB easier for JavaScript application developers with the features mentioned above.

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

Initially the components were linked together by relationship, but this ended up being very messy for a model. The components are in the `/lib` directory, which is the directory at the very top. The `/lib` directory contains all folders underneath. The folders are listed below:

| **Directory** | **Description**                                                           |
|---------------|---------------------------------------------------------------------------|
| `/lib`        | Contains Mongoose source code and JavaScript files that start the program |
| `/cast`       | Converts primitives and objects to other types                            |
| `/cursor`     | Used for table navigation                                                 |
| `/driver`     | Sets up connection information                                            |
| `/error`      | Error handling functions                                                  |
| `/helpers`    | Helper functions for use in other modules                                 |
| `/options`    | Populates interface with changeable options                               |
| `/plugins`    | Additional options users may install                                      |
| `/schema`     | Defines a MongoDB schema, which is like a table in SQL                    |
| `/types`      | Defines objects that may be used in Mongoose                              |


## Source Code Structures

![Codeline Model](img/codelineModel.png)

*Figure 2: Mongoose Source Code*

Our codeline model shows **all the source code** in the Mongoose repository.  Again, we used **directories** for the codeline model because directories are more in line with the scope of Mongoose’s architecture rather than individual files. Many folders, like `/lib`, have many directories underneath them as well. This diagram is shown above. There is a table below that also describes the codeline model more thoroughly.

| Root folder | Directory Level 1 | Directory Level 2     | Feature                                                                                                                                                                                                                     |
|-------------|-------------------|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /           |                   |                       | Contains everything of the Mongoose module, including library codes, test suites, documentations, example programs, and more.                                                                                               |
|             | .github/          |                       | Github repository-specific content, showing project funding channels, issue template, and pull request templates                                                                                                            |
|             |                   | workflow/             | Contain Github workflow files, such as automate running Mocha tests in the `test/` directory                                                                                                                                |
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

Mongoose library uses Mocha testing framework to test its codes. The testing files are located underneath the `test` folder, which is located in the root folder. Each named test file represent a module/feature being tested on (such as schema-related operations or special handling on specific data type values). This group attempted to run Mocha tests, either via IDE or command line, but only David Xie can successfully initiate Mocha tests via his WebStorm IDE by clicking on its run buttons; other group members did not observe any output (or experience non-test related errors) while attempting to run test files in VS Code IDE nor Node.js command line.

![Test Example](img/testExample.png)

*Figure 3: Example of Testing Code*

Many test files require the use of a common test file called `common.js`. This is located underneath the `/test` folder. Some outside dependencies include the `assert` library, the `collection` component located in the `/lib` folder, and some error validation (not pictured) which is located in the `error` component in `/lib`. Since `assert` is used, this means that Mongoose utilizes **unit testing** on individual components for their testing.

![common.js](img/commonTest.png)

*Figure 4: `common.js` Test File*

This `common.js` test file contains many functions that other testing files use. Figure 4 above shows the first few lines of `common.js`. Because this test file is well-defined and has common functions for use in other test files, this would be a great starting point to figure out how to test code for Mongoose.

![Testing Branches](img/differentBranches.png)

*Figure 5: Mongoose Branches*

Additionally, many developers use their own branches to test code. As of the time of fetching the repository, there are **over 100 different test branches**. Using branches allows developers to create pull requests for bug fixes and other improvements to the code. The Mongoose team would evaluate these pull requests and approve or deny changes if necessary.

# Applied Perspective

While Mongoose provides many advantages that promote its prevalence among JavaScript programs that need to interact with MongoDB, we choose to analyze Mongoose library’s **Performance Perspective**. Because Mongoose handles many queries (usually come from user-facing web information systems) on MongoDB, the performance of the system is very important to consider when looking at the architecture. The query speed should be fast so clients and users perform operations on MongoDB in a timely manner.

## Response Time

When JavaScript developers uses Mongoose, they will define a typed schema by using `new mongoose.Schema({...})` API similar to the one below, whereas each field are typed.

![API Schema](img/image10.png)

*Figure 6: API Schema*

However, when JavaScript programs add data to MongoDB using Mongoose, Mongoose will first attempt to cast the provided input to the predefined schema types by going through a series of if-statement checks (which would take extra time), even though the user adds a correct-typed value. The concern of slowed response time due to type checking and casting is least useful for a large and clean dataset, according to [this blog post](https://towardsdatascience.com/the-drastic-mistake-of-using-mongoose-to-handle-your-big-data-a3c408e21a4c).

For instance, if user pass in `false` (a boolean-typed value) at a table field that requires boolean value, according to lib/cast/boolean.js , Mongoose still need test whether `false` is within `Set([true, 'true', 1, '1', 'yes'])` to see whether false is a truthy value before testing whether this falsy value. As a result, Mongoose will have a higher response time to input a `false` value to the database compared to input a `true` value.

![](img/image15.png)

*Figure 7: Code snippet within `lib/cast/boolean.js file`*

As another example, when users want to insert a value to a String-typed field, Mongoose needs to first check whether the user passed in a null value or the user passed in the ID value of a document first, before checking whether this value can be casted to a String using the default `.toString()` method on an object. As a result, inserting an Object ID to a String-typed field takes less time (aka. reducing the database operations’ response time) compared to inserting a String-typed value to String-typed field; this issue is evident when we are inserting a large amount of data that is guaranteed to be String-typed (aka data is clean).

![](img/image11.png)

*Figure 8: Code snippet in `lib/cast/string.js`*

Side note on type casting and system predictability: the time consumption of type-casting processes is predictable, as all input values always go through <type>.js file to attempt casting value to the desired type (according to the type of schema). In addition, <type>.js files’ behaviors will not change during runtime, making type-casting operation stable, even though it reduces response time for Mongoose to insert values to MongoDB.

## Throughput

MongoDB is a document-based database, indicating its data can be unstructured. If information (and its data type) within a database cannot be relied upon due to a lack of schema consistency, then it is more challenging for JavaScript client developers  to interact with MongoDB databases even via Mongoose.

When using Mongoose, JavaScript client developers can set the database schema type while defining the table schema (such as declaring a String-typed column called `title`, in the below example). In contrast, developers need to explicitly define a typed-schema separately if they use native MongoDB syntax ([source](https://docs.mongodb.com/manual/core/schema-validation/#std-label-schema-validation-json)). Thus, the schema type enforcement reduces the client code’s need to add more code to check returned data (from database) and cast to client’s desired type.

![Schema Example](img/schemaExample.png)

*Figure 9: Example of a Schema*

This allows for correctness of the data type that users receive from queries. However, as a result of having many cast checks, these checks cause a drop in performance as a result. Someone had an example of a [benchmark performance between MongoDB and Mongoose](https://bugwheels94.medium.com/performance-difference-in-mongoose-vs-mongodb-60be831c69ad), and found that MongoDB can be faster at times. This may be due to the architecture of Mongoose, where it calls from multiple sources like in `lib/cast` to `lib/modules`, etc. This would [spell trouble for larger datasets](https://towardsdatascience.com/the-drastic-mistake-of-using-mongoose-to-handle-your-big-data-a3c408e21a4c) because of the reliance on multiple modules at once. Mongoose would certainly take a performance hit with large data.

## Applying the Perspective

### Performance Model
- User executes a query
- Query goes through a cast file for processing
- Cast file performs schema type checking and validation
- Cast file then returns requested data if the query was a find operation
- Otherwise, save data into database

![Performance Model](img/performance_model.png)

*Figure 10: Benchmark Data referenced from [source 1](https://blog.jscrambler.com/mongodb-native-driver-vs-mongoose-performance-benchmarks) and [source 2](https://github.com/Automattic/mongoose/issues/8751)*

### Identify the Performance-Critical Structure
In the diagram above, the performance-critical components start at the **model** query where depending on the user’s request (reading or writing to data), it can impact the performance for the rest of the process flow. Latency is further introduced by the **casting processor** which takes in the user input data and checks if it can be casted to the enforced types in the **Data Schema**. Finally, the `save()` operation is executed where the row is added to the **MongoDB database** collection.

### Identify the Key Performance Metrics
In the context of Mongoose, the key metrics to evaluate were reads/writes per second and the latency time. These metrics are the most important as read and write operations are the main ones that users perform with the system. For the benchmark, the Apache Benchmark suite was used where it would fire 150 requests per second from 4 concurrent users which would be a sufficient amount to see the extent of Mongoose’s throughput limit.

From the benchmark, it was found that Mongoose’s throughput was 583 reads/sec and 384 writes/sec. Its latency time was 1.71ms for reads and 2.60ms for writes. In contrast, the Native MongoDB driver's performance was significantly better with a throughput of 1200 reads/sec with 0.83ms latency and 1128 writes/sec with 0.89ms latency. This is not surprising due to the validation and type-casting processing that Mongoose needs to perform between reading or writing the given data. The latency performance loss can be significant though as one benchmark used a schema with over 750 types to validate. It was found to take around 22-30 seconds to finally save it into the database. However, disabling validation reduced the entire operation to less than 1 second. Overall, Mongoose represents a tradeoff between performance and functionality. When using Mongoose, the developer will expect degraded performance but can then obtain more features such as data validation, sanitization from possible injection attacks, and consistency within an enforced schema.

# Identify Styles and Patterns

## High-level architectural style
Mongoose applies the **Pipes and Filters architectural style**, where the flow of data is driven by data and the whole system is decomposed into components of data source, filters, pipes, and data sinks . The users’ query will select the input and Mongoose works as the filter, and the mongoDB is the result being fetch.

![Example of Pipes and Filters architectural style](img/Pipe.png)

*Figure 11: Example of Pipes and Filters architectural style*

## Decorator Pattern

By default, Mongoose will call create “automatically calls createIndex for each defined index in your schema” when connecting users’ apps to the MongoDB database. Users can optionally pass { autoIndex: false } as the second parameter on mongoose.connect(...) to disable this default behavior. Since this object alters Mongoose’s default behavior, Mongoose’s provided interface adheres to the decorator pattern.

Create a regular MongoDB connection:
`mongoose.connect('mongodb://user:pass@localhost:port/database');`

Create a MongoDB connection without having Mongoose call createIndex:

`mongoose.connect('mongodb://user:pass@localhost:port/database', { autoIndex: false });`

or

`mongoose.createConnection('mongodb://user:pass@localhost:port/database', { autoIndex: false });`

Link: [https://mongoosejs.com/docs/guide.html](https://mongoosejs.com/docs/guide.html)

## Iterator Pattern
Within lib/cursor, QueryCursor.js exposes JavaScript’s Streams3 interface, allowing client programs to call `.next()` function to conditionally (or in batch) advance to the next row/document of MongoDB’s table/collection. Since client programs can utilize cursor interface to iterate over content in MongoDB (a collection of objects) without any need to know Mongoose’s underlying implementation of cursor, Mongoose’s cursor interface is an example of Iterator pattern.

![](img/image21.png)

*Figure 12: [Cursor interface’s API documentation](https://mongoosejs.com/docs/api/query.html#query_Query-cursor)*

![](img/image34.png)

*Figure 13: Code snippet in `lib/cursor/QueryCursor.js`*

![](img/image30.png)

*Figure 14: Function Handling finding next Element in the Collection*

## Mediator Pattern

According to [documentation](https://mongoosejs.com/docs/tutorials/query_casting.html), when Mongoose fails to cast the passed in data type to the enforced data type in the schema, it throws an instance of the `CastError` class. Rather than handling the error processing themselves, the `castString` and `castBoolean` functions pass in the type, value, and path to the `CastError` class which serves as the mediator between the components. The `CastError` class then takes in the passed arguments and eventually returns the respective error message to be displayed back to the client. Therefore, this communication between different components (`lib/cast/string.js` and `lib/cast/boolean.js`) and the central authority, `CastError` class showcases the Mediator Pattern.

![Instance of CastError in "lib/cast/string.js"](img/CastErrorInstance.png)

*Figure 15: Instance of CastError in `lib/cast/string.js`*

![CastError class in “/lib/error/cast.js”](img/CastError.png)

*Figure 16: CastError class in `lib/error/cast.js`*

## Strategy Pattern

When declaring the table schema in Mongoose, Mongoose will accept commonly-used JavaScript data types such as `String`, `Number`, and `Boolean` and translate them into MongoDB schema types. This allows users to directly use JavaScript methods for this JavaScript data type and save the result to MongoDB.

According to the [documentation](https://mongoosejs.com/docs/validation.html#validation-errors), before running schema validators, Mongoose attempts to **coerce values to the correct type**. This process is called casting the document. If casting fails for a given path, the `error.errors` object will contain a `CastError` object.

In the source code itself, there are [some cast type conversions](https://mongoosejs.com/docs/schematypes.html). This can be seen in the below images, where a boolean converter converts commonly-used boolean values (but are not represented as a boolean data type value) into `true` or `false`.

![lib/cast/boolean.js example](img/castBooleanDotJs.png)

*Figure 17: Example of `lib/cast/boolean.js` (converts boolean-like string and number to true or false)*

The **strategy pattern** states that a family of algorithms should be encapsulated and interchangeable so the algorithms would vary for the clients that use them. Since clients may expect `true` or `false` values from varying strings, the logic would come from `boolean.js` and convert strings into boolean values. This follows a specific approach to casting for boolean values. Other methods exist for casting of other types such as strings and integers. This follows the **strategy pattern** closely because of multiple algorithms being made for similar functions.

![lib/schema/boolean.js example](img/schemaBooleanDotJs.png)

*Figure 18: Example of Strategy Pattern being put into place for booleans, `lib/schema/boolean.js`*

Likewise, if user wants to input data to a String-typed field, Mongoose will call `lib/cast/string.js` that handles casting values to String, of which Mongoose is using a different (casting) strategy.

# Architectural Assessment

## Open Close Principle

### a: files/modules in `lib/schema` folder
![Open Closed Principle 1](img/OpenClosed-1.png)

*Figure 19: `lib/schema` folder*

Instead of hard-coding data types of Mongoose schemas, Mongoose developers opted for processing each (supported) data type in separate files/modules. They are being referenced in `SchemaType(path, options, instance)` located in `./lib/schematype.js` . This allows MongoDB developers to create more files/modules to support new data types of MongoDB in the future.

![Open Closed Principle 1](img/OpenClosed-2.png)

*Figure 20: `SchemaType` function*

### b: `./lib/error` directory,
There are several error handling files that extend the `MongooseError` class , and the `MongooseError` class also extends the built-in JavaScript `Error` class. As a result, client classes (within Mongoose source code) can either use the `MongooseError` itself, or a more specific `Error` class that adds more behaviors to the `MongooseError` class, which is explained below.

![](img/image35.png)

*Figure 21: `MongooseError` class*

Example 1: `lib/error/divergentArray.js`
![](img/image12.png)

*Figure 22: `DivergentArrayError` class*

In the `DivergentArrayError` that extends `MongooseError`, it has a `super(msg)` function that calls functions within `MongooseError`. This coding style follows an open-closed principle as `DivergentArrayError` **extends** `MongooseError` instead of modifying `MongooseError` behaviors.

Example 2: `lib/error/cast.js`
![](img/image9.png)

*Figure 23: `CastError` class*

Like `DivergentArrayError`, `CastError` also extends `MongooseError` functionality by adding `CastError`’s specific behaviors, instead of modifying `MongooseError` behaviors.

### c: `lib/cast/boolean.js`
![](img/image27.png)

*Figure 24: `castBoolean` function*

In the `boolean.js` file, one can modify which values should be interpreted as `true` or `false` by modifying content in two `Set` objects, without the need to modify the actual boolean casting logic. As a result, one may choose to add the equivalent of “true” or “false” in other languages (such as “oui” or “non” in French) by adding them in the `convertToTrue` and `convertToFalse` `Sets`.

## Single Responsibility Principle
### a: `lib/schema` folder

![Open Closed Principle 1](img/OpenClosed-1.png)

*Figure 25: `lib/schema/operators` directory*

JavaScript files within `./lib/schema` handles data type (of the corresponding MongoDB schema types) individually (each JavaScript file handles own MongoDB data type). For instance, code handling String data type don’t need to know the code handling Date data type. Clients of Mongoose will define MongoDB schemas in a fashion similar to this:
```
const postSchema = new mongoose.Schema({
  url: String,
  description: String,
  username: String,
  likes: [String],
  created_date: Date
  })
```

### b: `lib/error/mongooseError.js` and Error classes (within the lib/error folder) that extend `MongooseError`.
![](img/image35.png)

*Figure 26: `MongooseError` class*

`MongooseError`’s sole responsibility is to throw an `Error` (built-in JavaScript `Error`) object with the name of “Mongoose”, allowing client program developers to easily distinguish error from Mongoose or other external modules (dependencies) when debugging their JavaScript programs.

## Dependency Inversion Principle

a: `.lib/cast.js`

![Dependency Inversion Principle 2](img/exampleOfDepency.png)

*Figure 27: `_cast` function*

Within `.lib/cast.js`, the function `_cast(val, numbertype, context)` assigns `numbertype.castForQuery({ val: item, context: context })` function to `val[nkey]` . However, depending on the content of `numbertype`, the client who invoke `castForQuery()` method will conditionally invoke different implementations of `castForQuery()` based on the schema data type (such as `castForQuery()` of `.lib/schema/date.js` or `.lib/schema/boolean.js`). Hence cast.js doesn't need to consider which implementation of `castForQuery()` should cast.js call as long as cast.js knows the data type of value that needs to be casted. Thus cast.js adheres to the dependency inversion principle.


## Principle of Least Knowledge (Law of Demeter)

### a: Mongoose Schema object creation
Mongoose provides an abstracted interface allowing JavaScript programs to interact with MongoDB (such as create a table and define a schema on this table) using Mongoose syntax instead of the MongoDB native syntax. Thus, clients don’t need to understand the internals of MongoDB syntax, as long as they can use Mongoose syntax correctly. Since Mongoose translates and forwards client requests to MongoDB, Mongoose’s provided interface adheres to the Law of Demeter principle.

![Law of Demeter 1](img/Demeter-1.png)

*Figure 28: example of Law of Demeter*

Here is an example of [database schema creation](https://mongoosejs.com/docs/guide.html) using Mongoose syntax
![](img/whodidthis1.png)

The MongoDB native syntax to create a table and [define a schema](https://docs.mongodb.com/manual/core/schema-validation/#std-label-schema-validation-json) for this table is similar to this:
![](img/whodidthis2.png)

In contrast, for JavaScript clients using mysql and mysql2 modules to interact with MySQL database, JavaScript clients need to use SQL query to perform database operations (highlighted part are SQL syntax, the rest of them are JavaScript syntax).
![app.get](img/whodidthis3.png)

## b: `lib/error/mongooseError.js` and Error classes (within the `lib/error` folder) that extend `MongooseError`.

![Law of Demeter 2](img/Demeter-2.png)

*Figure 29: another example of Law of Demeter*

Error-handling classes – such as `CastError`, `DivergentArrayError`, `MissingSchemaError`, `DocumentNotFoundError` – all extend the `MongooseError` object, and `MongooseError` extends the built-in JavaScript `Error` object. String, Boolean, and some other client classes interact with direct implementations of `MongooseError` rather than `MongooseError` itself, and these client classes do not need to know the behavior of `MongooseError` nor the built-in JavaScript `Error` Object. As a result, error-handling classes structures within Mongoose follow the Law of Demeter as well.

## Liskov Substitution Principle

### a: `lib/types/subdocument.js` that adds more behaviors to `lib/document.js`

For the **Liskov Substitution Principle**, there are two classes that promote this design pattern. These files are located in `lib/document.js`, which is the `Document` class, and `lib/types/subdocument.js`, which is the `SubDocument` class. See Figures 30 and 31 below.

![document.js](img/documentDotJs.png)

*Figure 30: `lib/document.js`*

![subdocument.js](img/subdocumentDotJs.png)

*Figure 31: `lib/types/subdocument.js`*

These two classes promote the *Liskov Substitution Principle* because the `SubDocument` could completely replace an instance of the `Document` class. This is because the `SubDocument` checks if there is a valid parent of itself. If there isn’t, then it just calls the `Document` class. This means that the `SubDocument` instance would just be a `Document` object. There is some extra logic when it does have a parent, but it still calls the `Document` class in the end.

## b: `checkRequired` functions in several `.js` files within `lib/schema`, and `checkRequired` function of `lib/schematype.js`
![checkRequired function in lib/schematype.js](img/Liskov-Substitution.png)

*Figure 32: `checkRequired` function in `lib/schematype.js`*

![Code of lib/schema/boolean.js](img/Liskov-Substitution1.png)

*Figure 33: Code of `lib/schema/boolean.js`*

![Code of lib/schema/number.js](img/Liskov-Substitution2.png)

*Figure 34: Code of `lib/schema/number.js`*

Within the `.lib/schema/operators` folder, `boolean.js` and `number.js` all use the same `checkRequired` function in `lib/schematype.js`. Thus this match the *Liskov Substitution Principle* because these “SubDocuments” replace and override the instance from the `schematype` class. For example, in `number.js`, it overrides the function the required validator uses to check whether a **string value** passes the ‘required’ check. While in `boolean.js`, they override the function the required validator uses to check whether a **boolean value** passes the ‘required’ check.

## Composite Reuse Principle

### a: `lib/cast/boolean.js`

![Composite Reuse Principle 1](img/CompReuse-1.png)
*Figure 35: example of Composite Reuse Principle 1`*

Within the `./lib/cast` folder, `boolean.js` uses an instance of `CastError` (`throw new CastError('boolean', value, path);` ) when it can’t convert a given value to a boolean value. Since `boolean.js` does not inherit the `CastError` itself and the `CastError` can exist by itself without `boolean.js` codes, `boolean.js` follows the Composite Reuse Principle.

### b: `lib/cast/string.js`

![](img/image8.png)
*Figure 36: code of `lib/cast/string.js`*

Within the `./lib/cast` folder, string.js also uses an instance of `CastError (throw new CastError('string', value, path); )` when it can’t convert a given value to a `String` value. This error throwing behavior in `string.js` is similar to `boolean.js` .

### c: `lib/schema.js`

![](img/image25.png)
*Figure 37: code of `lib/schema.js`*

Mongoose provides a `Schema.pick()` function allowing clients to “pick” a subset of schemas from the original schema. Mongoose will throw an instance of `MongooseError` object if the user does not pass an array in or the user's input is not in the original schema. Since this function does not inherit `MongooseError` but rather uses an instance of `MongooseError`, the `Schema.pick()` function favors composition over inheritance.

# System Improvement

## Refactoring:
- `lib/error/serverSelection.js` : clarify constant naming for error messages.
- `lib/schema.js` : in `Schema._clone()` function in line 336, group similar operations (within this function) together, use ES6 spread operators to favor modern JavaScript syntax.
- `test/model.create.test.js`: renamed the variable `B` to `testModel`, renamed variables `p` to either `returnPromise` or `callback`. This seemed necessary because p has two different functions, and B is not too specific of a variable name
- `lib/helpers/clone.js`: removed a confusing comment on lines 115-118 that just stated “ignore.”
- `lib/schema.js`: Initial comment for function at line 314 was redundant (Stated “returns a deep copy of the schema”). I converted the anonymous function to a named function called `schemaDeepCopy` so that the function’s purpose is more specific (and can therefore remove the details from the comment). Additionally renamed `s` const variable to schema for better readability as well

## Bug fix:
- [Github Issue 11515](https://github.com/Automattic/mongoose/issues/11515)
- `lib/helpers/pluralize.js` : use pluralize.js library (MIT-licensed) to rebase pluralization and irregular verb rules from pluralization.js to what’s currently in `Mongoose.js`, adjust Mongoose’s pluralize(str) function allowing developers to easily merge upstream pluralization rule changes on pluralization.js module to `Mongoose.js` .
- `test/helpers/pluralize.test.js` : writing test cases according to pluralization scenarios on the original issue post.
  - six => sixes
  - sex => sexes
  - vertex => vertices
  - Index => _indices_ (David Xie's fix)

## Feature improvement:
- `lib/cast/boolean.js` : Speed up in-practice runtime of boolean casting when the input values are clean (aka they are already a boolean value). In this case, no further data validation/processing should be there, and no `Set` initialization is needed (as (repeatedly) creating a `new` instance of object takes time)
  - `test/schema.boolean.test.js` : Writing more test cases to validate my code change does not break original boolean-casting features. New tests include whether `boolean.js` can cast non-boolean truthy value to true, and whether `boolean.js` throws an error when the user is trying to insert a non-boolean value to a boolean-typed schema field.
