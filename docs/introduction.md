## Intent Architect
This project was generated using Application templates created by the Intent Architect and The Delta platform team. Here is the link to the [Intent Architect website](https://intentarchitect.com/docs/articles/getting-started/welcome/welcome.html). For more information on the different application templates available and how they work, head over to The Delta Platform team's documentation on [gitbook](https://app.gitbook.com/o/-MhAHQRNbXRJJAmyAX--/s/mgu3uWRrevqSfLSu6Yml/platform-application-templates/overview)
 
## Clean CQRS API high level architecture
<img width="800" src="https://user-images.githubusercontent.com/103587065/168816156-460e98bf-f995-469d-9a56-fff45a63c903.png" />


## CQRS & MediatR
[CQRS](https://www.ibm.com/cloud/architecture/architectures/event-driven-cqrs-pattern/) is a pattern that splits the command and query responsibility into separate classes. This means that reads are sperate from writes. It aims to maximise performance, scalability and simplicity.

[MediatR](https://dotnetcoretutorials.com/2019/04/30/the-mediator-pattern-part-3-mediatr-library/) is a package that helps manage the flow of traffic in a manner that upholds the separation of concern principle and minimises dependencies. It simply uses handlers along with models to route traffic to the correct place. It also has built-in behaviours that can easily be attached before and/or after each request.

## Validation
All validation of requests is to be done using [fluent validator](https://fluentvalidation.net/). 


## Clean architecture

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
