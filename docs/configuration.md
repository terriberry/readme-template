# Configurations

Below are all the configurations for the project:


## Deployment environments
The deployment environment for the project is set by the ```ASPNETCORE_ENVIRONEMNT``` key stored inside the ```launchsettings.json``` file. By default, it is set to ```Local```, however, this can be set to ```Development``` or ```Production``` depending on the desired deployment environment to launch the project in:</br></br>

- ```Local```: Developer's desktop/workstation</br>
- ```Development```: Development server acting as a [sandbox](https://en.wikipedia.org/wiki/Sandbox_(software_development)) where unit testing may be performed by the developer</br>
- ```Production```: Serves end-users/clients</br>


## appsettings.json and environment variable
There are 2 places where configuration settings and keys can be stored, namely in the ```appsettings.json``` file and the ```environmentVariables``` key inside the ```launchsettings.json``` file.

Secret keys such as ```AWS_ACCESSKEY``` are stored inside the ```environmentVariables```  and general settings such as ```IpRateLimitOptions``` are stored inside ```appsettings.json```.


## Sentry
Sentry captures data by using an SDK within the application’s runtime. Here is a guide from their [website](https://docs.sentry.io/platforms/dotnet/).
All Sentry configurations are stored inside the ```appsettings.json``` file. Sentry is by default not enabled for the ```Local``` deployment environment.
> **DO NOT** enable Sentry for ```Local``` deployment environments</br>

Below are the available configuration parameters: </br>

**Required parameter:**</br>
- **SentryDsn**: Sentry automatically assigns you a Data Source Name (DSN) when you create a project to start monitoring events in your app. DSN tells the Sentry SDK where to send events so the events are associated with the correct project.</br>

**Optional parameters:**</br>
- **SentrySampleRate**: Configures the sample rate for error events, in the range of 0.0 to 1.0. The default is 1.0 which means that 100% of error events are sent. If set to 0.1 only 10% of error events will be sent. Events are picked randomly.


## Serilog & AWS CloudWatch

Serilog & AWS CloudWatch is only required if the the project is deployed in either the Development or Production environment, there is no need to log if hosted locally.</br>

Logging has been set up with [Serilog](https://serilog.net/) that performs console logging as well as logging to AWS CloudWatch. Default logging behaviour of requests and poor performance has already been configured. On top of this the following responses are automatically logged with error messages:
- 400 Bad Request
- 401 Unauthorised
- 403 Forbidden Access
- 404 Not Found
- 500 Internal Server Error

Additional logging is welcome as long as sensitive information is not divulged. Some good tips and hints on how to effectively log can be found [here](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html). Note that all unhandled exceptions are logged to [Sentry](https://sentry.io/welcome/?utm_source=google&utm_medium=cpc&utm_campaign=9575834316&content=445957162983&utm_term=sentry&gclid=Cj0KCQiAs5eCBhCBARIsAEhk4r54RrW4n0PC5i296nyraRtipzDHpVX2el6yWdkId9Vmz7KB6aq4Vc0aAixkEALw_wcB).


## PostgreSQL database connection

The PostgreSQL configuration is set in the ```appsettings.json```.</br>
Enter the PostgreSQL DB connection string details under ```""ConnectionStrings""```: </br></br>
```shell
  ""ConnectionStrings"": {
    ""DefaultConnection"": ""Host=localhost;Port=5432;Username=***;Password=***;Database=***;""
  }
```
Check that the database connection is successfully created by adding and running an initial migration.


## SQL Server database connection

The SQL Server configuration is set in the ```appsettings.json```.</br>
Enter the SQL Server DB connection string details under ```""ConnectionStrings""```:</br></br>
```shell
  ""ConnectionStrings"": {
    ""DefaultConnection"": ""Server=.;Initial Catalog=NewApplication104;Integrated Security=true;MultipleActiveResultSets=True""
  }
```
Check that the database connection is successfully created by adding and running an initial migration.

## In Memory database

The appsettings.jsons will not show any ConnectionString values since in-memory was chosen.


