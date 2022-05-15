  
<img position="right" src="https://bulungula-tech-centre.github.io/assets/images/team/delta.png" alt="drawing" width="150"/>

# Name of the project
> Additional information or tagline

A brief description of your project, what it is used for and how does life get
awesome when someone starts to use it.
</br></br></br>

## Installing / Getting started

Here is how to get the project up and running:

This project uses .NET ```6```. Make sure you have the correct .NET SDK installed in your machine. Run the following command to check the versions:

```shell
dotnet --list-sdks
```
Output similiar to the following appears:
```shell
3.1.100 [C:\program files\dotnet\sdk]
5.0.100 [C:\program files\dotnet\sdk]
6.0.100 [C:\program files\dotnet\sdk]
```

Hit F5 if using Visual Studio to build and run the project. If using the dotnet CLI, head to the directory containing the .sln file and run ```dotnet build```. After the project has built, head to the folder containing the Program.cs file and run ```dotnet run```.</br>
The project is by default running on localhost: ```http://localhost:xxxxx/```.
Swagger is pre-configured and will automatically route to ```http://localhost:xxxxx/index.html``` which displays the swagger doc
</br></br></br>

## Initial Configuration
Below are the initial configurations for the project: </br></br>

### Deployment environments
The deployment environment is set under ```ASPNETCORE_ENVIRONEMNT``` and is stored inside the ```launchsettings.json``` file. The environment can be set to ```Local```, ```Development``` or ```Production``` depending on what environment the application is at:</br>
```Local```: Developer's desktop/workstation</br>
```Development```: Development server acting as a [sandbox](https://en.wikipedia.org/wiki/Sandbox_(software_development) "Sandbox (software development)") where unit testing may be performed by the developer</br>
```Production```: Serves end-users/clients</br>

### appsettings.json
There will be different appsettings.json files depending on the different deployment environments the application is available for. The ```appsettings.json``` file for Local deployment environment will be: ```appsettings.Local.json```, for development: ```appsettings.Development.json``` and for production: ```appsettings.Production.json```.

### appsettings.json and environment variable
There are 2 places where configuration settings and keys can be stored namely the ```appsettings.json``` and the ```environmentVariables``` inside the ```launchsettings.json```.
Secret keys such as ```AWS_ACCESSKEY``` are stored inside the ```environmentVariables```  and general settings such as ```IpRateLimitOptions``` are stored inside ```appsettings.json```.

### Sentry
Sentry captures data by using an SDK within your application’s runtime. Here is a guide from their [website](https://docs.sentry.io/platforms/dotnet/).
All the configurations are stored inside the ```appsettings.json``` file. </br>





### Serilog 


### PostgreSQL database connection

By default, the database is configured as in-memory, this is configured in the appsettings.json:
```shell
"UseInMemoryDatabase": "true",
"ConnectionStrings": {
 "DefaultConnection": "Host=localhost;Port=5432;Username=***;Password=***;Database=***;"
}
```
To swop this out for a PostgreSQL database, set ```"UseInMemoryDatabase"``` to ```false``` and enter the PostgreSQL DB connection string details under ```"ConnectionStrings"```



### SQL Server database connection


By default, the database is configured as in-memory, this is configured in the appsettings.json:
```shell
"UseInMemoryDatabase": "true",
"ConnectionStrings": {
  "DefaultConnection": "Server=.;Initial Catalog=NewApplication3;Integrated Security=true;MultipleActiveResultSets=True"
}
```
To swop this out for a SQL Server database, set ```"UseInMemoryDatabase"``` to ```false``` and enter the SQL Server DB connection string details under ```"ConnectionStrings"```
</br></br></br>

## Developing
Below are steps required to start developing an existing project created using Intent Architect:

### Install and setup Intent Architect
The first thing that is required before any dev work is to install and setup Intent Architect. A detailed guide on how to do this is documented [here](https://app.gitbook.com/o/-MhAHQRNbXRJJAmyAX--/s/wlBDkDmB9NnayT8MEoDa/platform-application-templates/setup). Below is a short summary of the steps in the guide:</br>
>**Step 1**: Head over to the download page from Intent Architect [here](https://intentarchitect.com/#/downloads) and download and install the latest version of the software</br></br>
**Step 2**: Notify the Platform team that you are registering a new account with Intent Architect. Once confirmed with the team, create an account with Intent Architect using this [link](https://intentarchitect.com/#/user-access/register) and then log in</br></br>
**Step 3**: Clone the Clean CQRS application template repo from The-Delta-Studio Github repo [here](https://github.com/The-Delta-Studio/dpfm-modules-dotnet)</br></br>
**Step 4**: Head into the local repo which will be called ```dpfm-modules-dotnet``` and build the ```TDS.Modules.sln``` solution file</br></br>
**Step 5**: Lastly, add the path of the ```Intent.Modules``` folder i.e. ```../dpfm-modules-dotnet/Intent.Modules``` into Asset Repositories under settings in Intent Architect and give it a name e.g. ```TDS Clean API```

This is a very short summary and is intended to give an overview of the Intent Architect installation and setup process. Head over to the documentation link given above for a full step by step guide.

### Working with an existing project in Intent
In most cases, the project will have already been created, and you are required to continue with the development. Below are the steps to get you started with an already existsing project:</br>
>**Step 1**: Start by cloning the project from the Github repo into your local machine </br></br>
**Step 2**: Open the ```.isln``` file, this will open Intent Architect with the necessary files for the project. The ```.isln``` file is placed inside the ```intent``` folder</br></br>
**Step 3**: Open the ```.sln``` file inside the IDE of your choice.  This is the codebase for the project. Now you have the recommended setup in place i.e. the ```.isln``` open in Intent Architect and ```.sln``` open in the IDE of choice</br></br>
**Step 4**: In Intent Architect, the entity classes are designed and built using UML class diagrams and this can be accessed by clicking on ```Domain``` in the left sidebar menu. The business logic such as CRUD and endpoints can be accessed and modified by clicking on ```Services``` in the left sidebar menu</br></br>
**Step 5**: After making changes in Intent Architect, save this by pressing ```⌘ + S``` or ```Ctrl + S``` and run the Software Factory and apply the staged changes. More information about Software Factory is given under the ```Running the software factory``` section below

This is the general work flow using the Intent Architect software i.e. make domain and service layer changes using the designers in Intent Architect, run the software factory to implement the changes and run the code inside the IDE of choice.</br></br>

For more information on how the development process with Intent Architect works, [here](https://app.gitbook.com/o/-MhAHQRNbXRJJAmyAX--/s/wlBDkDmB9NnayT8MEoDa/platform-application-templates/the-template-runbooks/custom-logic-apis/clean-architecture-cqrs-api/open-a-pre-existing-project) is a detailed guide that shows this step by step.


### Running the software factory
The Software Factory is where the magic happens. When run by pressing ```F5```, or simply by clicking ```Run Software Factory```, the following process is initiated:
1. Examines the changes made in the Domain and Service designers (the entity classes, the business logic etc.)
2. Auto-generates and modifies the necessary C# files to implement the changes
3. Lists all the files generated and modified into a staging environment which you can examine
4. Allows you to choose the files to apply the changes and when you click ```APPLY CHANGES```, the change/s are automatically implemented in the codebase

 
### Running migrations
The entity classes in code and the database schema are decoupled during development. And therefore migration is used to incrementally sync the entity classes with the database schema. EF Core is the ORM that performs the migrations and it generates the necessary migration files to implement the changes. [Here](https://docs.microsoft.com/en-us/ef/core/managing-schemas/migrations/?tabs=vs) is an overview of migrations using EF Core from Microsoft for more information.</br></br>

Every time there is a change to the entity classes (by using the Domain designer in Intent Architect), the entity classes in the codebase will be out of sync with the database. In order to sync, perform the migrations as follows:
>**Step 1**: Head over to the ```.Infrastructure``` folder in the codebase in the IDE of choice. This is where the database context: ```ApplicationDbContext.cs``` is stored </br></br>
>**Step 2**: In case there are multiple deployment environments 
>Using **dotnet CLI**:
>```shell
>dotnet ef 
>```



### Adding business logic


### Create a new project using Intent


### Initial configurations


**Required parameter:**</br>
**SentryDsn**: Sentry automatically assigns you a Data Source Name (DSN) when you create a project to start monitoring events in your app. DSN tells the Sentry SDK where to send events so the events are associated with the correct project.</br>

**Optional parameters:**</br>
**SentrySampleRate**: Configures the sample rate for error events, in the range of 0.0 to 1.0. The default is 1.0 which means that 100% of error events are sent. If set to 0.1 only 10% of error events will be sent. Events are picked randomly.


## Introduction

### Intent architect
This project was generated using Application templates created by the Intent Architect and The Delta platform team. Here is the link to the [Intent Architect website](https://intentarchitect.com/docs/articles/getting-started/welcome/welcome.html). For more information on how the Application templates work, head over to the documentation on [gitbook](https://app.gitbook.com/o/-MhAHQRNbXRJJAmyAX--/s/mgu3uWRrevqSfLSu6Yml/platform-application-templates/overview)

### ASP.NET Core



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
