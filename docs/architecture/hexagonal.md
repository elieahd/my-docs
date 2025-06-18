## Hexagonal Architecture 

Hexagonal Architecture is a software design pattern that emphasizes separation of concerns, testability, and flexible infrastructure integration. 

It focuses on isolating the core business logic from external systems like databases, UIs, and APIs.

![hexagonal architecture](../assets/hexagonal-architecture.png)

#### Core domain 

This is the center of the hexagon, and contains : Business rules, Domain models, Application services (use cases).

It should not depend on any framework or external technology.

#### Ports (Interfaces)

Ports define how the application expects to interact with the outside world.

There are two types:

* Inbound Ports: Interfaces used to enter the application (e.g., use case interfaces, controller service interfaces)
* Outbound Ports: Interfaces the application uses to communicate outward (e.g., repository interfaces, messaging service interfaces)

#### Adapters

Adapters implement the ports.

There are two types:

* Inbound Adapters: Trigger the application (e.g., REST controllers, CLI handlers, message listeners)
* Outbound Adapters: Provide implementations for outbound ports (e.g., JPA repositories, REST clients, Kafka producers)

## Project structure 

```
├── domain
├────── entities
├────── inbound (ports)
├────── outbound (ports)
├────── services
├── infrastructure 
├───── inbound (adapters)
├──────── rest
├──────── queues
├──────── batches
├──────── cli
├──────── ...
├───── outbound (adapters)
├──────── database 
├──────── queues
├──────── bucket
├──────── ...
└── 
```

## Use case : Blogger 

Let's take a use case about designing a blogging platform that allow publish content in the form of posts.

In the traditional architecture we would found ourself with the current structure 

```
├── models
├────── Category
├────── Post
├── repositories
├────── CategoryRepository
├────── PostRepository
├── services
├────── CategoryService
├────── PostService
├── controllers
├────── PostController
├────── CategoryController
├── BloggerApplication
└── 
```

check current branch : [`traditional`](todo) 

To apply the hexagonal architecture to current use case, we would end up with the following structure 


```
├── domain
├────── entities
├────────── Category
├────────── Post
├────── inbound
├────────── CreatePost
├────────── SearchPost
├────────── GetCategories
├────── outbound
├────────── CategoryInventory
├────────── PostInventory
├────── services
└── 
```

### Unit testing with in stubs (in memory adapter)

### Unit testing the architecture with ArchUnit 

