# Clean Architecture - Patterns, Practices and Principles - Pluralsight course by Matthew Renze

### Module 1 - Course overview

Course overview
- Clean Architecture
- Domain-centric Architecture
- Application Layer
- Commands and Queries
- Functional Organization
- Microservices
- Testable Architecture
- Evolving the Architecture

* * *

### Module 2 - Introduction

Purpose of the course
- Philosophy of architectural essentialism - way of designing an architecture around what’s essential vs. what’s just a detail
- Set of patterns, practices and principles 
- Alternative to traditional architecture (3 layered db architecture)

Focus
- Enterprise applications
- Agile architecture
- Top 7 ideas

Audience
- Developers
- Architects

What is Clean Code?

What is Software Architecture?
- High-level (at least higher level than the code we write)
- Structure - how things are organised. 
- Layers - vertical partitions of the system
- Components - horizontal partitions within each layer 
- Relationships - how they are all wired together

Levels of Architectural Abstraction

This course will be covering mostly layers and components and bit of sub-systems when covering microservices

Messy vs. Clear Architecture - Spaghetti vs. Lasagna

What is Bad Architecture?
- Complex - accidental instead of essential complexity
- Incoherent - parts don’t seem like they fit together
- Rigid - resists change or difficult to evolve
- Brittle - touching one part of code here, breaks somewhere else
- Untestable - architecture fights you when you try to write unit and integration tests even though you want to write them
- Unmaintainable - all the above leads to this

What is Good Architecture?
- Simple - or at least only as complex as it is necessary
- Understandable - easy to reason about the software as a whole
- Flexible - easy to adapt the system to meet changing requirements
- Emergent - evolves over the life of the project
- Testable - makes testing easier
- Maintainable - ultimately all of the above make the software more maintainable over the life of the project

What is Clean Architecture?
Architecture that is designed for the inhabitants of the architecture (users, developers building and maintaining the system)… not for the architect (put aside his or her own desires and wishes and design what’s best for the inhabitants of the system)… or the machine (optimise first for the inhabitants and only optimise for the machine when necessary, i.e., we want to avoid premature optimisation). Clean architecture is a philosophy of architectural essentialism. It’s about focusing on what’s truly essential to the software’s architecture instead of the implementation detail. 

Why invest in Clean Architecture?
- Cost / benefit 
    - Minimise cost (of creation and maintenance)
    - Maximise (business) value 
- Overall goal thus, is to maximise ROI 
- Focus on the essential - mirrors use cases of the mental models of the users by embedding them in both arch and code 
- Build only what is necessary, when necessary - only build features and corresponding architecture that are necessary to solve immediate need to avoid accidental complexity, unnecessary features, premature performance optimisations and arch embellishments
- Optimise for maintainability - enterprise apps last a long time and a significant amount of time and resources are spent in maintaining, so it makes sense to optimise for maintainability. 

Decisions, decisions, decisions…
- Answers to most questions to an architect is “it depends"
    - Context is king
    - All decisions are a tradeoff
    - Align with business goals

***

### Module 3 - Domain-centric Architecture

##### Overview 
- Domain-centric architecture and how it varies from database-centric architecture
- Types of Domain-centric architectures
- Pros and Cons

##### Domain-centric Architecture

DBCA - architecture revolved around the database. Lately, there has been shift towards making the Domain the center and considering the db as just an implementation detail

“The first concern of the architect is to make sure that the house is usable, it is not to ensure that the house is made of brick.” - Uncle Bob

What is essential vs. detail? 

E.g. while building a house:
- Space is essential
- Usability is essential
- Building material is a detail
- Ornamentation is a detail

Similarly, we need to look at what is essential for the inhabitants of the architecture
- Domain is essential - without it the system will not represent the mental models of the users
- Use cases are essential 
- Presentation is a detail - JS vs [ASP.NET](http://ASP.NET) MVC is just a detail
- Persistence is a detail - SQL vs NoSQL db is just a detail. They are important yes, but not more than the essentials which are about solving the problems of the users. 

##### Domain-centric architectures

Hexagonal Architecture

[Hexagonal archiecture](img.png)

Onion Architecture

[Onion Architecture](img.png)

No inner layer knows about the outer layer. 

The Clean Architecture

[The Clean Architecture](img.png)

All 3 architectures have roughly the same benefits. Essentially, they put the domain model at the center, wrap it in an application layer which embeds the use cases, adapts the application to implementation details and all dependencies should point inwards towards the domain. 

##### Pros and Cons
Pros
- Focus on domain =&gt; puts inhabitants’ needs at the center =&gt; cost reductions in maintaining the software
- Less coupling between domain logic and implementation detail =&gt; more flexible and adaptable =&gt; more easily evolved
-  Allows for Domain Driven Design (DDD) - which is a great set of strategies for handling high degree of complexity

Cons
- Change is difficult - most are taught only the traditional 3-layered db-centric architecture 
- Requires more thought to implement a domain-centric design - it requires thinking about what classes belong in the domain layer, vs. what classes belong in the application layer rather than placing everything in the business logic layer
- Initial higher cost compared to a db-centric architecture but eventually pays off. 

* * *

### Module 4 - Application Layer

##### Overview
- Application Layer - learn about architectures with an application layer and how it differs from the traditional 3-layered architecture
- Dependency Inversion Principle - which helps make arch more flexible and maintainable
- Pros and Cons

##### What are Layers?

Boundaries and Vertical partitions of an application designed to 
- Represent different levels of abstraction
- Maintain the single-responsibility principle
- Isolate developer roles and skills
- Help support multiple implementations
- Assist with varying rates of change

Essentially, layers are how we slice the application into manageable units of complexity

##### Classic Three-layer Architecture

Suitable for basic CRUD applications. 

##### Modern Four-layer Architecture

##### Application layer 
- Implements use cases as executable code - e.g., shopping cart code
- High-level application logic - e.g., command that adds an item to a shopping cart
- Knows about the domain layer
- No knowledge of other layers like presentation, persistence or infrastructure layers. 
- Contains interfaces for dependencies
- Then we use an IoC (Inversion of control) framework and dependency injection to wire up all the interfaces and their implementations at runtime

##### Layer dependencies

Dependency inversion - abstractions should not depend on details, rather, details should depend on abstractions. Hence the arrow from infrastructure to application and persistence to application instead of the other way around. 

Inversion of control - that is, the dependencies oppose the flow of control in our application, which provides several benefits like
- Independent deployability - i.e., we can replace the implementation in product without affecting  the dependencies 
- Flexible and maintainable - for e.g., we can swap out our persistence and infrastructure dependencies without having negative side effects ripple throughout the application and domain layers

Sometimes we may need to add an additional dependency from the persistence to the domain when using an Object Relational Mapper. This is necessary for the ORM to map the domain entities into tables in the database since the persistence layer needs to know about the domain entities. But using an ORM is optional but saves a tremendous amount of time. 

##### Why use an Application Layer?

Pros
- Focus on use cases
- Embed use cases as high-level executable code - easy to understand
- Follows DIP - makes code more flexible and lets us decide implementation details until later

Cons
- Additional layer cost - generally we want to keep the number of layers small
- Requires extra thought on what belongs in application layer and what belongs in domain layer rather than just throwing it all in business logic layer
- IoC is counter-intuitive initially 

***

---

### Module 5 - Commands and Queries

##### Overview
* Commands and Queries - and how we strive to keep them apart in our architecture
* CQRS Architectures - 3 types
* Pros and Cons of CQRS practices
* Demo

##### Command-Query Separation
* 1988 - Bertrand Meyer 
* Command 
    * Does something 
    * Should modify state 
    * Should not return value
* Query
    * Answers question
    * Should not modify state
    * Should return value
* Should keep these two apart to avoid nasty side effects that hide in methods that violate this principle
* As Martin Fowler points out, this is not always possible. 
    * For e.g., stack.pop() - it both removes item (command) and returns the top item (query). 
    * Or when creating a new record - create record (command), return created record’s id (query). 
    * So there are clear exceptions to this rule but in general we should strive to keep the two apart

##### CQRS Architectures 
* Expands the CQ separation to the architectural level
* _TODO: insert image from Evernote_
* Queries should be optimised for reading data; Commands should be optimised for writing data - this improves performance and the clarity of the code
* Persistence - ORM like Hibernate; Data Access - ORM projections
* Single database CQRS (refer image above)
    * Single database
    * Commands use domain
    * Queries use database
    * Simplest of the 3
* Two-database CQRS
    * _TODO: insert image from Evernote_
    * Read and write database
    * Commands use write DB (3NF)
    * Queries use read DB (read optimised like 1NF)
    * Eventual consistency 
    * Orders of magnitude faster for reads
* Event Sourcing CQRS
    * _TODO: insert image from Evernote_
    * Store events
        * Historical records of all events stored in a persistence medium called an event store
    * Replay events 
    * Modify entity
    * Store new event
    * Update read database
    * Benefits 
        * Complete audit trail
        * Point-in-time reconstruction
        * Replay events
            * Useful for load and stress testing
        * Multiple read database 
        * Rebuild production database just by replaying
    * Significant additional expense if you don’t need any of the above features

##### Pros and Cons
* Pros
    * More efficient design
    * Optimised performance
    * Event sourcing benefits
* Cons
    * Inconsistent across stacks - command stack vs query stack
    * 2 db arch potentially introduces eventual consistency
    * Event sourcing introduces cost to create and maintain the event sourcing features

##### Demo
_video_

---


### Module 6 - Functional Organization

##### Overview
* Screaming Architecture 
* Functional vs. Categorial cohesion
* Pros and Cons of Functional Organization
* Demo

##### Screaming Architecture
* “The architecture should scream the intent of the system!” - Uncle Bob
    * We do this by organising the architecture around the use cases of the system.
* We can organise our application’s folder structure and namespaces according to the components that are used to build the software - like Models, Views and Controllers or we can organise according to the use cases of the system, concepts pertaining to user’s interactions with the objects of the system like Customers, Products and Vendors
* Model your application folder structure like a multi-storeyed building - each layer of architecture corresponds to a floor in the building. Keep components that belong to the following categories near to each other
    * Persistence and Infrastructure layer / folder
    * Domain layer / folder
    * Application layer / folder
    * Presentation layer / folder

##### Pros and Cons
* Pros
    * Spatial locality - components that are used together live together. For e.g., forks, spoons and knives live together instead of eating fork, tuning fork near each other because they are both forks
    * Easy to navigate - looking for Employee related classes would be easy because one just needs to navigate to the Employee folder in the presentation layer and are all contained there
    * Avoid vendor lock-in - not forced to use the directory structure recommended by the framework
* Cons
    * Lose framework conventions
    * Lose automatic scaffolding provided by framework
    * Categorical is easier at first but makes things worse later

##### Demo
_video_

---

### Module 7 - Microservices

##### Overview
* Bounded Context - how they can be used to sub-divide a domain model
* Microservices - sub-divide a monolithic app
* Pros and Cons
* Demo

##### Components
* This is how we sub-divide our application once it grows beyond a manageable size
* When we model classes that are applicable in multiple contexts, things don’t feel right because there are properties or methods that make sense in one context but not in others

##### Bounded Context
* It is the recognition of a specific contextual scope within which a specific model is valid
* _TODO: insert image from Evernote_ 
    * Employee model is split into Sales Person and Support Person classes
    * Then we transfer state using clearly defined interfaces using either coordinated transactions or using an eventual consistency model

##### Microservices
* Subdivide monolithic applications into smaller subsystems
* Communicate between each other using clearly defined interfaces typically using light-weight web protocols - JSON over HTTP via REST APIs
* Helps divide large teams into smaller teams - say, 1 micro service per team
* Makes the sub-systems independent allowing for separate tech stack that’s appropriate for each microservice
* Independently deploy and scale as needed
* Similar in concept to service-oriented architectures
* 2 common questions
    * How big should each microservice be? 
    * Where should I draw the boundary for each microservice?
    * This is where Bounded Contexts come in. Microservices have natural alignment to bounded contexts. 
    * Ideally we want each microservice, each domain, each database and each development team to line up - maximises cohesion, minimises coupling. Allows team to focus on single domain. 
    * Still large debate on how small a microservice should be. 

##### Pros and Cons
* Pros
    * Flatter cost curve compared to monoliths - cost of building microservices up front is larger but it grows slowly as the system grows. So for projects with large domains, project lifecycles, in theory microservices are appropriate
    * High cohesion and low coupling
    * Independence - practices, deployment, tech
* Cons
    * Higher up-front cost
    * Conway’s Law - orgs which design systems are constrained to produce systems that mirror the communication structures of their orgs. So your org structure should be compatible with your architecture. Microservices are suitable for agile teams whose org is not setup as a bureaucratic top-down non-autonomous styles
    * Distributed system costs - network latency, fault tolerance, load balancing and more. 


##### Demo
_video_

---


### Module 8 - Testable Architecture

##### Overview
* Test-Driven Development
* Test Automation Pyramid
* Pros and Cons
* Demo

##### The Current State of Testing
* Despite advancements in technology and the awareness around the practice, many software developers still practice
    * Very little testing
    * Ineffective testing
    * Inefficient testing
* And the reasons include
    * Not enough time
    * Not my job
    * It’s too hard to create good tests as the architecture makes it difficult to add tests
* The module covers how clean architecture makes testing easier. In addition how TDD drives the design of a clean architecture. 

##### Test-Driven Development
* Write a failing test first and use this to drive the design of the architecture - Red, Green, Refactor
    1. Create a failing test
    2. Get the test to pass by writing minimal code
    3. Improve the code
* You end up creating a comprehensive suite of tests
* Drives testable design as the design of the class is driven by passing the tests
* More maintainable
* Eliminates fear that making changes will break the code
* Key component for creating a testable architecture

##### Types of tests
* Based on what they are testing
    * Unit tests
    * Integration tests
    * Component tests
    * Service tests
    * UI tests
* Based on why they are testing
    * Functional tests
    * Acceptance tests
    * Smoke tests
    * Exploratory tests
* Based on how they are testing
    * Automated tests
    * Semi-automated tests
    * Manual tests

##### Test Automation Pyramid
* _TODO: insert image from Evernote_
* Focus on creating many low-cost unit tests, medium-cost service tests, few high-cost UI tests and very few manual tests
* Acceptance tests - 
    * verify functionality; 
    * Language of product owners; 
    * criteria for completeness; 
    * full tests are problematic
    * Eliminate user interface
    * Eliminate database
* This helps us to 
    * Eliminate dependencies
    * Focus on the essential 
    * Smoke test instead for high-cost UI tests
    * Minimize manual tests
    * Let testers focus on exploratory tests instead to provide high quality UX for users

##### Pros and Cons
* Pros
    * Easier to test
    * Improves design => more maintainable
    * Eliminates fear to make changes
* Cons - there should be hardly any reason to not have tests, but for the sake of counter-argument
    * Higher up-front cost
    * TDD requires discipline
    * Requires team buy-in

##### Demo
_video_

---

### Module 9 - Evolving the Architecture

##### Overview
* Evolving the Architecture over the lifecycle of the project to reduce the risk of uncertainties
* More info on architectural styles mentioned in the course
* Course wrap-up

##### Evolving the Architecture
* Last responsible moment - delay decisions until the cost of not making the decision is greater than the cost of making the decision. By doing so, we 
    * Make informed decisions; avoid premature optimisations
* Deciding too early is a risk
* Deciding too late is a risk
* Eliminate risk early 
    * For e.g., by focusing on the domain and application logic in solving the user problems we can validate whether or not software will provide enough user value before investing in implementation details
* Clean architecture will help survive through the following
    * Technology may change
    * Markets may change
    * Preferences may change
* Pros of building an evolutionary architecture
    * Embraces uncertainty
    * Embraces change - inevitable 
    * Reduces certain types of risk
* Cons
    * Assumes uncertainty - but usually this is the case with large apps
    * Assumes instability - but usually this is the case with large apps
    * Still has limitations

##### Where to go next
* Recommended books
    * Patterns of Enterprise Application Architecture, 2003, Martin Fowler
    * Clean Architecture, Uncle Bob
    * Domain-Driven Design, Eric Evans
    * Dependency Injection in .NET, Mark Seaman
* Pluralsight courses
    * Domain-Driven Design Fundamentals - Steve Smith and someone else
    * Domain-Driven Design in Practice
    * Modern Software Architecture
    * Microservices Architecture
    * Dependency Injection On-Ramp
* Websites
    * http://martinfowler.com
    * CQRS: goodenoughsoftware.net; udidahan.com; 
    * http://www.matthewrenze.com

----

