  
<img position="right" src="https://bulungula-tech-centre.github.io/assets/images/team/delta.png" alt="drawing" width="150"/>

# Name of the project
> Additional information or tagline

A brief description of your project, what it is used for and how does life get
awesome when someone starts to use it.
</br></br></br>

## Installing and running the project 

Here is how to get the project up and running on your local machine:

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

## Configurations

If you are developing on an existing project, most of the **configurations below will already have been set** during the initial project creation process. The configurations are listed here to let the developer know where everything is stored and also for developers that are creating new projects using Intent, who will need to set the initial configurations.


### Deployment environments
The deployment environment for the project is set by the ```ASPNETCORE_ENVIRONEMNT``` key stored inside the ```launchsettings.json``` file. This can be set to ```Local```, ```Development``` or ```Production``` depending on the desired deployment environment:</br></br>

- ```Local```: Developer's desktop/workstation</br>
- ```Development```: Development server acting as a [sandbox](https://en.wikipedia.org/wiki/Sandbox_(software_development) "Sandbox (software development)") where unit testing may be performed by the developer</br>
- ```Production```: Serves end-users/clients</br>

### appsettings.json template
There will be different appsettings.json files depending on the different deployment environments the application is available for. For example, for the 3 deployment environments listed above, the appsettings.json will be: ```appsettings.Local.json```, ```appsettings.Development.json``` and ```appsettings.Production.json``` respectively.

When creating the project for the first time using Intent, the appsettings.json template will be create for you. Create the specific appsettings.json file depending on the deployment environment options available and copy paste the template code and make the necessary changes.

### appsettings.json and environment variable
There are 2 places where configuration settings and keys can be stored namely the ```appsettings.<deployment env>.json``` and the ```environmentVariables``` inside the ```launchsettings.json```.
Secret keys such as ```AWS_ACCESSKEY``` are stored inside the ```environmentVariables```  and general settings such as ```IpRateLimitOptions``` are stored inside ```appsettings.<deployment env>.json```.

### Sentry
Sentry captures data by using an SDK within the application’s runtime. Here is a guide from their [website](https://docs.sentry.io/platforms/dotnet/).
All Sentry configurations are stored inside the ```appsettings.<deployment env>.json``` file. </br>

Below are the available configuration parameters: </br></br>

**Required parameter:**</br>
- **SentryDsn**: Sentry automatically assigns you a Data Source Name (DSN) when you create a project to start monitoring events in your app. DSN tells the Sentry SDK where to send events so the events are associated with the correct project.</br>

**Optional parameters:**</br>
- **SentrySampleRate**: Configures the sample rate for error events, in the range of 0.0 to 1.0. The default is 1.0 which means that 100% of error events are sent. If set to 0.1 only 10% of error events will be sent. Events are picked randomly.


### Serilog & AWS CloudWatch

Serilog & AWS CloudWatch is only required if the the project is deployed in either the Development or Production environment, there is no need to log if hosted locally.</br></br>

Logging has been set up with [Serilog](https://serilog.net/) that performs console logging as well as logging to AWS CloudWatch. Default logging behaviour of requests and poor performance has already been configured. On top of this the following responses are automatically logged with error messages:
- 400 Bad Request
- 401 Unauthorised
- 403 Forbidden Access
- 404 Not Found
- 500 Internal Server Error

Additional logging is welcome as long as sensitive information is not divulged. Some good tips and hints on how to effectively log can be found [here](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html). Note that all unhandled exceptions are logged to [Sentry](https://sentry.io/welcome/?utm_source=google&utm_medium=cpc&utm_campaign=9575834316&content=445957162983&utm_term=sentry&gclid=Cj0KCQiAs5eCBhCBARIsAEhk4r54RrW4n0PC5i296nyraRtipzDHpVX2el6yWdkId9Vmz7KB6aq4Vc0aAixkEALw_wcB).

### PostgreSQL database connection

By default, the database is configured as in-memory, this is configured in the ```appsettings.json```:
```shell
"UseInMemoryDatabase": "true",
"ConnectionStrings": {
 "DefaultConnection": "Host=localhost;Port=5432;Username=***;Password=***;Database=***;"
}
```
To swop this out for a PostgreSQL database, set ```"UseInMemoryDatabase"``` to ```false``` and enter the PostgreSQL DB connection string details under ```"ConnectionStrings"```.</br></br>

Check that the database connection is successfully created by adding and running an initial migration. Details on how to run migrations is detailed under ```Running migrations``` under ```Developing using Intent Architect``` below.



### SQL Server database connection


By default, the database is configured as in-memory, this is configured in the ```appsettings.json```:
```shell
"UseInMemoryDatabase": "true",
"ConnectionStrings": {
  "DefaultConnection": "Server=.;Initial Catalog=NewApplication3;Integrated Security=true;MultipleActiveResultSets=True"
}
```
To swop this out for a SQL Server database, set ```"UseInMemoryDatabase"``` to ```false``` and enter the SQL Server DB connection string details under ```"ConnectionStrings"```</br></br>

Check that the database connection is successfully created by adding and running an initial migration. Details on how to run migrations is detailed under ```Running migrations``` under ```Developing using Intent Architect``` below.
</br></br></br>

## Developing using Intent Architect
Below are steps required to start developing an **existing project** created using Intent Architect:

### Install and setup Intent Architect
The first thing that is required before any dev work can begin is the installation and setup of Intent Architect. A detailed guide on how to do this is documented [here](https://app.gitbook.com/o/-MhAHQRNbXRJJAmyAX--/s/wlBDkDmB9NnayT8MEoDa/platform-application-templates/setup). Below is a short summary of the steps in the guide:</br>
>**Step 1**: Head over to the download page from Intent Architect [here](https://intentarchitect.com/#/downloads) and download and install the latest version of the software</br></br>
**Step 2**: Notify the Platform team that you are registering a new account with Intent Architect. Once confirmed with the team, create an account with Intent Architect using this [link](https://intentarchitect.com/#/user-access/register) and then log in</br></br>
**Step 3**: Clone the Clean CQRS application template repo from The-Delta-Studio Github repo [here](https://github.com/The-Delta-Studio/dpfm-modules-dotnet)</br></br>
**Step 4**: Head into the local repo which will be called ```dpfm-modules-dotnet``` and build the ```TDS.Modules.sln``` solution file</br></br>
**Step 5**: Lastly, add the path of the ```Intent.Modules``` folder i.e. ```../dpfm-modules-dotnet/Intent.Modules``` into Asset Repositories under settings in Intent Architect and give it a name e.g. ```TDS Clean API```

A reminder that, this is a very short summary and is intended to give an overview of the Intent Architect installation and setup process. Head over to the documentation link given above for a step by step guide.

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

Before this step, make sure the database is connected. Instructions on how to configure the database is given above under the ```Configurations``` section.</br>
The entity classes in code and the actual database are decoupled during development. And therefore migrations are used to incrementally sync the entity classes with the database. EF Core is used. [Here](https://docs.microsoft.com/en-us/ef/core/managing-schemas/migrations/?tabs=vs) is an overview of migrations using EF Core for more information.</br>

Below are the steps:
>**Step 1**: There may be multiple deployment environments set up for the project and to prevent accidentally migrating to the wrong environment, explicitly state the deployment environment by running ```$env:ASPNETCORE_ENVIRONMENT='<environment e.g. Local>'``` for Visual Studios package manager, ```export ASPNETCORE_ENVIRONMENT='<environment e.g. Local>'``` for Mac on terminal and ```setx ASPNETCORE_ENVIRONMENT "<environment e.g. Local>" /M``` for Windows in cmd</br></br>
>**Step 2**: Head over to the ```.Infrastructure``` folder in the codebase in the IDE of choice. This is where the database context: ```ApplicationDbContext.cs``` is stored</br></br>
>**Step 3**: Add the migration:
>Using **dotnet CLI**:
>```shell
>dotnet ef --startup-project <path to .Api folder> migrations add <migration name>
>```
>```--startup-project``` is required becasue the database context and the actual project live in different folders. <path to .Api folder> refers to the location of the ```.Api``` folder i.e. ```../<projectName>.Api```.</br>
>Using **Visual Studio package manager**:
>```shell
>Add-Migration <migration name>
>```


### Adding business logic
This is where CRUD, DTOs, validations, endpoints amongst other are designed and implemented. Here is a [link](https://app.gitbook.com/o/-MhAHQRNbXRJJAmyAX--/s/wlBDkDmB9NnayT8MEoDa/platform-application-templates/the-template-runbooks/custom-logic-apis/clean-architecture-cqrs-api/add-your-business-logic) to a detailed guide to show you how this is done step by step.

### Creating a new project using Intent
If you decide to create an entirely new project using Intent Architect, here is the [link](https://app.gitbook.com/o/-MhAHQRNbXRJJAmyAX--/s/wlBDkDmB9NnayT8MEoDa/platform-application-templates/the-template-runbooks/custom-logic-apis/clean-architecture-cqrs-api/create-and-configure-the-project) to show to exactly how to do this.


## Introduction

### Intent Architect
This project was generated using Application templates created by the Intent Architect and The Delta platform team. Here is the link to the [Intent Architect website](https://intentarchitect.com/docs/articles/getting-started/welcome/welcome.html). For more information on the different application templates available and how they work, head over to The Delta Platform team's documentation on [gitbook](https://app.gitbook.com/o/-MhAHQRNbXRJJAmyAX--/s/mgu3uWRrevqSfLSu6Yml/platform-application-templates/overview)

### CQRS & MediatR
[CQRS](https://www.ibm.com/cloud/architecture/architectures/event-driven-cqrs-pattern/) is a pattern that splits the command and query responsibility into separate classes. This means that reads are sperate from writes. It aims to maximise performance, scalability and simplicity.

[MediatR](https://dotnetcoretutorials.com/2019/04/30/the-mediator-pattern-part-3-mediatr-library/) is a package that helps manage the flow of traffic in a manner that upholds the separation of concern principle and minimises dependencies. It simply uses handlers along with models to route traffic to the correct place. It also has built-in behaviours that can easily be attached before and/or after each request.

### Validation
All validation of requests is to be done using [fluent validator](https://fluentvalidation.net/). 


### Clean architecture

Clean architecture is an established API architecture that focuses on splitting up the API into separate layers that contain different purposes. These layers are as follows:
 - Domain Layer
 - Application Layer
 - Infrastructure Layer
 - UI/API Layer

These layers have strict dependency rules working from the outside in. This means that the **domain layer is dependant on none of the others**, the **application layer only dependent on the domain layer** and finally **the infrastructure and UI/API layer dependant only on the application layer**:

<img src="https://jasontaylor.dev/wp-content/uploads/2020/01/Figure-01-2.png" alt="drawing" width="400" />

The domain layer contains enterprise-wide logic and types including: 
 - Data Models (entities)
 - Value Objects
 - System-wide interfaces and utility classes
 - Some exceptions (eg. data specific exceptions)
 
The application layer contains all business logic and types including:
 - Interfaces
 - Models
 - Logic
 - Commands/Queries
 - Validators
 - Exceptions
 - Behaviours
 - Mapping
 
The infrastructure layer handles all external concerns such as: 
  - Persistence (data layer and ORMs)
  - Identity (or other auth providers)
  - File System
  - System Clock
  - External Gateways to API Clients
  - Cache
  - Migrations

The UI/API Layer contains the interface of the application to the outside world. It consists of the Web API framework including:
- controllers
- middleware
- startup
- amongst others
