
<img position="right" src="https://bulungula-tech-centre.github.io/assets/images/team/delta.png" alt="drawing" width="150"/>

# Name of the project
> Additional information or tagline

A brief description of your project, what it is used for and how does life get
awesome when someone starts to use it.

## Installing / Getting started

Here is how to get the project up and running:

**VS Code**

This project uses .NET ```5```. Make sure you have the correct .NET SDK installed in your machine. Run the following command to check the versions:

```shell
dotnet --list-sdks
```
Output similiar to the following appears:
```shell
3.1.100 [C:\program files\dotnet\sdk]
5.0.100 [C:\program files\dotnet\sdk]
6.0.100 [C:\program files\dotnet\sdk]
```

Head to the directory containing the Program.cs file and run the following commands
```shell
dotnet build
dotnet run
```
```dotnet build``` will compile the project for the first time.
If the project compiles correctly, running ```dotnet run``` returns an output similiar to this:
```shell
info: Microsoft.Hosting.Lifetime[14]
      Now listening on: https://localhost:7089
info: Microsoft.Hosting.Lifetime[14]
      Now listening on: http://localhost:5095
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
      Hosting environment: Development
info: Microsoft.Hosting.Lifetime[0]
      Content root path: /Users/terrilee/Documents/Delta/practiceBE/minimalAPIPractice1/
```
The project is running on localhost on ```https://localhost:7089```.
Swagger is automatically configured and can be accessed by appending the localhost url with: ```/swagger/index.html```. For example: ```https://localhost:7089/swagger/index.html```.


### Initial Configuration
***
#### Sentry
Sentry captures data by using an SDK within your application’s runtime. Here is the setup guide from their [website](https://docs.sentry.io/platforms/dotnet/)

Install the NuGet package to add the Sentry dependency:

**dotnet core cli**
```shell
dotnet add package Sentry -v 3.17.1
```
Configuration should happen as early as possible in your application's lifecycle.

Initialize in the Main method in Program.cs:
```C#
using Sentry;

using (SentrySdk.Init(o =>
{
    o.Dsn = "https://examplePublicKey@o0.ingest.sentry.io/0";
    o.MaxBreadcrumbs = 50;
    o.Debug = true;
})
{
    // app code here
}
```
**Dsn**: Sentry automatically assigns you a Data Source Name (DSN) when you create a project to start monitoring events in your app. DSN tells the Sentry SDK where to send events so the events are associated with the correct project.</br></br>
**Debug**: Turns debug mode on or off. If debug is enabled SDK will attempt to print out useful debugging information if something goes wrong with sending the event. The default is always false.</br></br>
**MaxBreadcrumbs**: This variable controls the total amount of breadcrumbs that should be captured. This defaults to 100.

***

#### PostgreSQL database connection

***

#### SQL Server database connection



## Developing

Here's a brief intro about what a developer must do in order to start developing
the project further:


### Building

If your project needs some additional steps for the developer to build the
project after some code changes, state them here:

```shell
./configure
make
make install
```

Here again you should state what actually happens when the code above gets
executed.

### Deploying / Publishing

In case there's some step you have to take that publishes this project to a
server, this is the right time to state it.

```shell
packagemanager deploy awesome-project -s server.com -u username -p password
```

And again you'd need to tell what the previous code actually does.

## Introduction

### Intent architect
This project was generated using Application templates created by the Intent Architect and The Delta platform team. Here is the link to the [Intent Architect website](https://intentarchitect.com/docs/articles/getting-started/welcome/welcome.html). For more information on how the Application templates work, head over to the documentation on [gitbook](https://app.gitbook.com/o/-MhAHQRNbXRJJAmyAX--/s/mgu3uWRrevqSfLSu6Yml/platform-application-templates/overview)


### Clean architecture

Clean architecture is a well-etablished API architecture that focusses on splitting up the API into separate layers that contain different purposes. These layers are as follows:
 - Domain Layer
 - Application Layer
 - Infrastructure Layer
 - UI/API Layer

Note that these layers have strict dependency rules working from the outside in. This means that the **domain layer is dependant on none of the others**, the **application layer only dependent on the domain layer** and finally **the infrastructure and UI/API layer dependant only on the application layer**

<img src="https://jasontaylor.dev/wp-content/uploads/2020/01/Figure-01-2.png" alt="drawing" width="400" />

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

### CQRS & MediatR
[CQRS](https://www.ibm.com/cloud/architecture/architectures/event-driven-cqrs-pattern/) is a pattern that splits the command and query responsibility into separate classes. This means that reads are sperate from writes. It aims to maximise performance, scalability and simplicity.

[Mediatr](https://dotnetcoretutorials.com/2019/04/30/the-mediator-pattern-part-3-mediatr-library/) is a package that helps manage the flow of traffic in a manner that upholds the separation of concern principle and minimises dependencies. It simply uses handlers along with models to route traffic to the correct place. It also has built-in behaviours that can easily be attached before and/or after each request.

### Database Info and ORM
This section details information about the database itself and how the API manages and interacts with it.

#### Migrations
Migrations are managed by [DbUp](https://dbup.readthedocs.io/en/latest/). The migration manager is a separate application within the infrastructure layer and is designed to be easily run by pipelines. One simply needs to run the script and it will take care of the rest. In order to add migrations, SQL scripts must be generated by the developer and copied into the scripts folder according to naming conventions. For naming conventions see the Delta API Standards section on migrations standards.

#### Database
The template is configured with a PostgreSQL database. PGAdmin is recommended to be installed for database management and querying of data during development.

#### Data Access
##### Repository Layer

### Delta API Standards
See below for some standards that must be adhered to when building on top of this API template.

#### Migrations 
Migrations in the template are managed by DbUp in a separate Infrastructure.Migrations application within the solution. In order to run the migrations one simply needs to run the application and it will handle the rest. It is recommended that this is automated into the pipelines themselves. The commands that are run are as follows:

`dotnet build <project path and name>/Infrastructure.Db.Migrator/Infrastructure.Db.Migrator.csproj`  
`dotnet run <project path and name>/Infrastructure.Db.Migrator/Infrastructure.Db.Migrator.csproj`

In order to add new scripts to the project the raw sql was my coded and added as a sql file into the scripts folder. By default all sql scripts are embedded into the project. Please note the naming convention for sql scripts as described in the section below.

##### Naming Standards
The following naming convention must be applied to all migration scripts:

    <unix datetime in seconds>_<table description>_<operation description>.sql
    <unix datetime in seconds>_<view name>_<operation description>.sql
    <unix datetime in seconds>_<procedure name>_<operation description>.sql
    <unix datetime in seconds>_<function name>_<operation description>.sql

#### Auditable Entity
All entities should inherit from the base auditable entity to ensure certain base columns appear on all database tables. These columns include: 
 - CreatedAt
 - CreatedBy
 - LastModified
 - LastModifiedBy
 - DeletedAt
 - DeletedBy

Note that the assigning of values to these objects is automatically handled by the framework.

#### Containerizing
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


##### Container environmental variables
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

#### Validation
All validation of requests is to be done using [fluent validator](https://fluentvalidation.net/). 

#### Logging
Logging has been set up with [Serilog](https://serilog.net/) that performs console logging as well as logging to AWS CloudWatch. Default logging behaviour of requests and poor performance has already been configured. On top of this the following responses are automatically logged with error messages:
- 400 Bad Request
- 401 Unauthorised
- 403 Forbidden Access
- 404 Not Found
- 500 Internal Server Error

Additional logging is welcome as long as sensitive information is not divulged. Some good tips and hints on how to effectively log can be found [here](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html)

Note that all unhandled exceptions are logged to [Sentry](https://sentry.io/welcome/?utm_source=google&utm_medium=cpc&utm_campaign=9575834316&content=445957162983&utm_term=sentry&gclid=Cj0KCQiAs5eCBhCBARIsAEhk4r54RrW4n0PC5i296nyraRtipzDHpVX2el6yWdkId9Vmz7KB6aq4Vc0aAixkEALw_wcB). It is required that the Sentry project must be set up to notify a slack channel of all non-local exceptions.

Performance of long-running transactions and transactions in the baserepository is also monitored in sentry and can be viewed under the performance monitoring tab of the project. The default samplerate is set to 0.0 for safety reasons and should be adjusted to the rate required by your project.



## Features

What's all the bells and whistles this project can perform?
* What's the main functionality
* You can also do another thing
* If you get really randy, you can even do this

## Configuration

Here you should write what are all of the configurations a user can enter when
using the project.

#### Argument 1
Type: `String`  
Default: `'default value'`

State what an argument does and how you can use it. If needed, you can provide
an example below.

Example:
```bash
awesome-project "Some other value"  # Prints "You're nailing this readme!"
```

#### Argument 2
Type: `Number|Boolean`  
Default: 100

Copy-paste as many of these as you need.

## Contributing

When you publish something open source, one of the greatest motivations is that
anyone can just jump in and start contributing to your project.

These paragraphs are meant to welcome those kind souls to feel that they are
needed. You should state something like:

"If you'd like to contribute, please fork the repository and use a feature
branch. Pull requests are warmly welcome."

If there's anything else the developer needs to know (e.g. the code style
guide), you should link it here. If there's a lot of things to take into
consideration, it is common to separate this section to its own file called
`CONTRIBUTING.md` (or similar). If so, you should say that it exists here.

## Links

Even though this information can be found inside the project on machine-readable
format like in a .json file, it's good to include a summary of most useful
links to humans using your project. You can include links like:

- Project homepage: https://your.github.com/awesome-project/
- Repository: https://github.com/your/awesome-project/
- Issue tracker: https://github.com/your/awesome-project/issues
  - In case of sensitive bugs like security vulnerabilities, please contact
    my@email.com directly instead of using issue tracker. We value your effort
    to improve the security and privacy of this project!
- Related projects:
  - Your other project: https://github.com/your/other-project/
  - Someone else's project: https://github.com/someones/awesome-project/


## Licensing

One really important part: Give your project a proper license. Here you should
state what the license is and how to find the text version of the license.
Something like:

"The code in this project is licensed under MIT license."
