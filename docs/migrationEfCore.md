# Running migrations using EF Core

The entity classes in code and the actual database are decoupled during development. And therefore migrations are used to incrementally sync the entity classes with the database. EF Core is used for migrations. [Here](https://docs.microsoft.com/en-us/ef/core/managing-schemas/migrations/?tabs=vs) is an overview of migrations using EF Core for more information and [here](https://app.gitbook.com/o/-MhAHQRNbXRJJAmyAX--/s/wlBDkDmB9NnayT8MEoDa/platform-application-templates/the-template-runbooks/custom-logic-apis/clean-architecture-cqrs-api/build-your-domain-layer/add-and-run-migrations) is a link to the Platform team's detailed documentation on how to perform the migrations.</br>

Before this step, make sure of the following:

1. the database is connected. Instructions on how to configure the database is given above under the ```Configurations``` section.</br>
2. the ```UseInMemory``` key is set to ```false```

</br>

## Steps

>**Step 1**: There may be multiple deployment environments set up for the project and to prevent accidentally migrating to the wrong environment, explicitly state the deployment environment by running:
>- Visual Studios package manager: ```$env:ASPNETCORE_ENVIRONMENT='<environment e.g. Local>'```</br>
>- Mac on terminal: ```export ASPNETCORE_ENVIRONMENT='<environment e.g. Local>'```</br>
>- Windows in cmd: ```setx ASPNETCORE_ENVIRONMENT "<environment e.g. Local>" /M```</br>
>
>**Step 2**: Head over to the ```.Infrastructure``` folder in the codebase in the IDE of choice. This is where the database context: ```ApplicationDbContext.cs``` is stored</br></br>
>**Step 3**: Add the migration:\
>Using **dotnet CLI**:
>```shell
>dotnet ef --startup-project <path to .Api folder> migrations add <migration name>
>```
>>Note: ```--startup-project``` is required becasue the database context and the actual project live in different folders. <path to .Api folder> refers to the location of the ```.Api``` folder i.e. ```../<projectName>.Api```
>
>Using **Visual Studio package manager**:
>```shell
>Add-Migration <migration name>
>```
>**Step 4**: Inspect the migration file  generated by intent inside the ```Migrations``` folder</br></br>
>**Step 5**: Run the migration:
>Using **dotnet CLI**:
>```shell
>dotnet ef --startup-project <path to .Api folder> database update
>```
>Using **Visual Studio package manager**:
>```shell
>Update-Database
>```

## Migration Naming Standards

Below is the migration naming standard. Depending on the type of operation that is being performed on the database, choose between the 4 options below:

>1. Table operation:\
>\<unix datetime in seconds\>\_tb\_\<insert table description\>\_\<insert operation description\>
>2. View operation:\
>\<unix datetime in seconds\>\_vw\_\<insert view name\>\_\<insert operation description\>
>3. Stored procedure operation:\
>\<unix datetime in seconds\>\_sp\_\<insert procedure name\>\_\<insert operation description\>
>4. Function operation:\
>\<unix datetime in seconds\>\_fn\_\<insert function name\>_\<insert operation description\>

The \<unix_datetime_in_seconds\> is autogenerated by EF Core, therefore, don't include this when specifying the migration name.

An example:

Using **dotnet CLI**:
>```shell
>dotnet ef --startup-project ../PetStore.Api migrations add tb_Pets_AddedMoreAttributes
