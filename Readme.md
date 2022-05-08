
# tds-clean-api-template

## Introduction
API template for all Delta projects based on Clean Architecture principles. Some background on the pattern can be found here 
- [Clean Architecture Video with Jason Taylor](https://www.youtube.com/watch?v=5OtUm1BLmG0&feature=youtu.be)
- [Uncle Bob Clean Architecture](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)
- [Jason Taylor Getting Started](https://jasontaylor.dev/clean-architecture-getting-started/)
- [Clean Architecture Example - Jason Taylor](https://github.com/jasontaylordev/CleanArchitecture)
- [Northwind Traders (Example)](https://github.com/jasontaylordev/NorthwindTraders)

### Clean Architecture
Clean architecture is a well-etablished API architecture that focusses on splitting up the API into separate layers that contain different purposes. These layers are as follows:
 - Domain Layer
 - Application Layer
 - Infrastructure Layer
 - UI/API Layer

Note that these layers have strict dependency rules working from the outside in. This means that the **domain layer is dependant on none of the others**, the **application layer only dependent on the domain layer** and finally **the infrastructure and UI/API layer dependant only on the application layer**

![Clean Architecture Basics](https://jasontaylor.dev/wp-content/uploads/2020/01/Figure-01-2.png)

#### Domain Layer
The domain layer contains enterprise-wide logic and types including: 
 - Data Models (entities)
 - Value Objects
 - System-wide interfaces and utility classes
 - Some exceptions (eg. data specific exceptions)
 
#### Application Layer
The application layer contains all business logic and types as can be seen below:
 - Interfaces
 - Models
 - Logic
 - Commands/Queries
 - Validators
 - Exceptions
 - Behaviours
 - Mapping
 
#### Infrastrucutre Layer 
The infrastructure layer handles all external concerns such as: 
  - Persistence (data layer and ORMs)
  - Identity (or other auth providers)
  - File System
  - System Clock
  - External Gateways to API Clients
  - Cache
  - Migrations

#### UI/API Layer
This contains the interface of the application to the outside world. In this template, it consists of the Web API framework including controllers, middleware and startup amongst others. 

### CQRS & Mediatr
[CQRS](https://www.ibm.com/cloud/architecture/architectures/event-driven-cqrs-pattern/) is a pattern that splits the command and query responsibility into separate classes. This means that reads are sperate from writes. It aims to maximise performance, scalability and simplicity.

[Mediatr](https://dotnetcoretutorials.com/2019/04/30/the-mediator-pattern-part-3-mediatr-library/) is a package that helps manage the flow of traffic in a manner that upholds the separation of concern principle and minimises dependencies. It simply uses handlers along with models to route traffic to the correct place. It also has built-in behaviours that can easily be attached before and/or after each request.

## Updates to the Template
Note that all updates to the template will only take effect once they are merged into master. All updates require at least 3 reviews with two of these being made by a senior developer. 

## How to Use the Template

## Database Info and ORM
This section details information about the database itself and how the API manages and interacts with it.

### Migrations
Migrations are managed by [DbUp](https://dbup.readthedocs.io/en/latest/). The migration manager is a separate application within the infrastructure layer and is designed to be easily run by pipelines. One simply needs to run the script and it will take care of the rest. In order to add migrations, SQL scripts must be generated by the developer and copied into the scripts folder according to naming conventions. For naming conventions see the Delta API Standards section on migrations standards.

### Database
The template is configured with a PostgreSQL database. PGAdmin is recommended to be installed for database management and querying of data during development.

### Data Access
#### Repository Layer

## Delta API Standards
See below for some standards that must be adhered to when building on top of this API template.

### Migrations 
Migrations in the template are managed by DbUp in a separate Infrastructure.Migrations application within the solution. In order to run the migrations one simply needs to run the application and it will handle the rest. It is recommended that this is automated into the pipelines themselves. The commands that are run are as follows:

`dotnet build <project path and name>/Infrastructure.Db.Migrator/Infrastructure.Db.Migrator.csproj`  
`dotnet run <project path and name>/Infrastructure.Db.Migrator/Infrastructure.Db.Migrator.csproj`

In order to add new scripts to the project the raw sql was my coded and added as a sql file into the scripts folder. By default all sql scripts are embedded into the project. Please note the naming convention for sql scripts as described in the section below.

#### Naming Standards
The following naming convention must be applied to all migration scripts:

    <unix datetime in seconds>_<table description>_<operation description>.sql
    <unix datetime in seconds>_<view name>_<operation description>.sql
    <unix datetime in seconds>_<procedure name>_<operation description>.sql
    <unix datetime in seconds>_<function name>_<operation description>.sql

### Auditable Entity
All entities should inherit from the base auditable entity to ensure certain base columns appear on all database tables. These columns include: 
 - CreatedAt
 - CreatedBy
 - LastModified
 - LastModifiedBy
 - DeletedAt
 - DeletedBy

Note that the assigning of values to these objects is automatically handled by the framework.

### Containerizing
In order to spin up the application in a docker container, a dockerfile has been provided in the API project. 

Spinning up the container involves:
1. Building it from the tds-clean-api-template\tds-clean-api-template directory with the following command :
````
docker build -t tds-clean-api-template -f API\Dockerfile .
````
2. Running the container with this command:
````
docker run -p 8080:80 --name tds-clean-api-template-local tds-clean-api-template
````
Notes: 
- The dockerfile exposes port 80 which is then forwarded to port 8080. This means that the app will be available on http://localhost:8080.
- The period at the end of the build command is to indicate the context is the current directory, not for grammar in this markdown file.


#### Container environmental variables
The environmental variables can be added to the Dockerfile, or via the commandline while running docker. 

To add variables to the Dockerfile can be done with the header ENV:
````
ENV DATABASE_CONNECTION_STRING=XXXX
````

To add to the docker run command, add via the -e flag: 
````
-e DATABASE_CONNECTION_STRING=XXXX 
````
Take note that in a Local environment the database host should change from localhost to host.docker.internal.

### Validation
All validation of requests is to be done using [fluent validator](https://fluentvalidation.net/). 

### Logging
Logging has been set up with [Serilog](https://serilog.net/) that performs console logging as well as logging to AWS CloudWatch. Default logging behaviour of requests and poor performance has already been configured. On top of this the following responses are automatically logged with error messages:
- 400 Bad Request
- 401 Unauthorised
- 403 Forbidden Access
- 404 Not Found
- 500 Internal Server Error

Additional logging is welcome as long as sensitive information is not divulged. Some good tips and hints on how to effectively log can be found [here](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html)

Note that all unhandled exceptions are logged to [Sentry](https://sentry.io/welcome/?utm_source=google&utm_medium=cpc&utm_campaign=9575834316&content=445957162983&utm_term=sentry&gclid=Cj0KCQiAs5eCBhCBARIsAEhk4r54RrW4n0PC5i296nyraRtipzDHpVX2el6yWdkId9Vmz7KB6aq4Vc0aAixkEALw_wcB). It is required that the Sentry project must be set up to notify a slack channel of all non-local exceptions.

Performance of long-running transactions and transactions in the baserepository is also monitored in sentry and can be viewed under the performance monitoring tab of the project. The default samplerate is set to 0.0 for safety reasons and should be adjusted to the rate required by your project.

## Unit testing
Unit testing has been set up with [XUnit](https://xunit.net/) as the testing tool and [Moq](https://github.com/Moq/moq4/wiki/Quickstart) as the mocking framework.

[AutoFixture](https://github.com/AutoFixture/AutoFixture) is used to easily create test data during the [Arrange](https://docs.microsoft.com/en-us/visualstudio/test/unit-test-basics?view=vs-2019#write-your-tests) phase of a test and helps with maintainability.

[Fluent Assertions](https://fluentassertions.com/) provides extention methods to improve readability during the Assert phase of a test.

### Base tests
This template contains tests for repository setup and base commands, queries and their respective validators.

### Executing tests
Once navigated to the solution folder, the command used to run the unit tests is `dotnet test`

For more information, see [here](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-test).

### Naming conventions
Unit test method names follow the convention of 

**Should_**_ExpectedResult__**When_**_StateUnderTest_
#### Examples
````
Should_ReturnTrue_When_EntityCreated()

Should_HaveError_When_FindByIsNull()

Should_ThrowException_When_CreatedByIsNull()
````

