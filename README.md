<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://user-images.githubusercontent.com/103587065/176515593-58d005dc-65a2-4638-994f-f9f79c9b0fe2.png">
  <source media="(prefers-color-scheme: light)" srcset="https://user-images.githubusercontent.com/103587065/176515498-8625721d-f468-40f2-b2d1-003442145e1f.png">
  <img alt="The Delta Studio Logo" position="right" align="right" width=300>
</picture>

# Name of the project
> Additional information or tagline

A brief description of your project, what it is used for and how does life get
awesome when someone starts to use it.
</br></br>

## Introduction
[Here](docs/introduction.md) are the fundamental concepts relevant to the project

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


## Configurations

[Here](docs/configuration.md) is the list of all the configuration options for this project.


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


### Adding business logic
This is where CRUD, DTOs, validations, endpoints amongst other are designed and implemented. Here is a [link](https://app.gitbook.com/o/-MhAHQRNbXRJJAmyAX--/s/wlBDkDmB9NnayT8MEoDa/platform-application-templates/the-template-runbooks/custom-logic-apis/clean-architecture-cqrs-api/add-your-business-logic) to a detailed guide to show you how this is done step by step.

### Creating a new project using Intent
If you decide to create an entirely new project using Intent Architect, here is the [link](https://app.gitbook.com/o/-MhAHQRNbXRJJAmyAX--/s/wlBDkDmB9NnayT8MEoDa/platform-application-templates/the-template-runbooks/custom-logic-apis/clean-architecture-cqrs-api/create-and-configure-the-project) to show to exactly how to do this.

 
### Migrations
Migrations are done using Entity Framework Core. [Here](docs/migrationEfCore.md) is a link that details how to perform the migration


