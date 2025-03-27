# BambangShop Publisher App
Tutorial and Example for Advanced Programming 2024 - Faculty of Computer Science, Universitas Indonesia.

---

## About this Project
In this repository, we have provided you a REST (REpresentational State Transfer) API project using Rocket web framework.

This project consists of four modules:
1.  `controller`: this module contains handler functions used to receive request and send responses.
    In Model-View-Controller (MVC) pattern, this is the Controller part.
2.  `model`: this module contains structs that serve as data containers.
    In MVC pattern, this is the Model part.
3.  `service`: this module contains structs with business logic methods.
    In MVC pattern, this is also the Model part.
4.  `repository`: this module contains structs that serve as databases and methods to access the databases.
    You can use methods of the struct to get list of objects, or operating an object (create, read, update, delete).

This repository provides a basic functionality that makes BambangShop work: ability to create, read, and delete `Product`s.
This repository already contains a functioning `Product` model, repository, service, and controllers that you can try right away.

As this is an Observer Design Pattern tutorial repository, you need to implement another feature: `Notification`.
This feature will notify creation, promotion, and deletion of a product, to external subscribers that are interested of a certain product type.
The subscribers are another Rocket instances, so the notification will be sent using HTTP POST request to each subscriber's `receive notification` address.

## API Documentations

You can download the Postman Collection JSON here: https://ristek.link/AdvProgWeek7Postman

After you download the Postman Collection, you can try the endpoints inside "BambangShop Publisher" folder.
This Postman collection also contains endpoints that you need to implement later on (the `Notification` feature).

Postman is an installable client that you can use to test web endpoints using HTTP request.
You can also make automated functional testing scripts for REST API projects using this client.
You can install Postman via this website: https://www.postman.com/downloads/

## How to Run in Development Environment
1.  Set up environment variables first by creating `.env` file.
    Here is the example of `.env` file:
    ```bash
    APP_INSTANCE_ROOT_URL="http://localhost:8000"
    ```
    Here are the details of each environment variable:
    | variable              | type   | description                                                |
    |-----------------------|--------|------------------------------------------------------------|
    | APP_INSTANCE_ROOT_URL | string | URL address where this publisher instance can be accessed. |
2.  Use `cargo run` to run this app.
    (You might want to use `cargo check` if you only need to verify your work without running the app.)

## Mandatory Checklists (Publisher)
-   [ ] Clone https://gitlab.com/ichlaffterlalu/bambangshop to a new repository.
-   **STAGE 1: Implement models and repositories**
    -   [✓] Commit: `Create Subscriber model struct.`
    -   [✓] Commit: `Create Notification model struct.`
    -   [✓] Commit: `Create Subscriber database and Subscriber repository struct skeleton.`
    -   [✓] Commit: `Implement add function in Subscriber repository.`
    -   [✓] Commit: `Implement list_all function in Subscriber repository.`
    -   [✓] Commit: `Implement delete function in Subscriber repository.`
    -   [✓] Write answers of your learning module's "Reflection Publisher-1" questions in this README.
-   **STAGE 2: Implement services and controllers**
    -   [✓] Commit: `Create Notification service struct skeleton.`
    -   [✓] Commit: `Implement subscribe function in Notification service.`
    -   [✓] Commit: `Implement subscribe function in Notification controller.`
    -   [✓] Commit: `Implement unsubscribe function in Notification service.`
    -   [✓] Commit: `Implement unsubscribe function in Notification controller.`
    -   [✓] Write answers of your learning module's "Reflection Publisher-2" questions in this README.
-   **STAGE 3: Implement notification mechanism**
    -   [✓] Commit: `Implement update method in Subscriber model to send notification HTTP requests.`
    -   [✓] Commit: `Implement notify function in Notification service to notify each Subscriber.`
    -   [ ] Commit: `Implement publish function in Program service and Program controller.`
    -   [ ] Commit: `Edit Product service methods to call notify after create/delete.`
    -   [ ] Write answers of your learning module's "Reflection Publisher-3" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Publisher) Reflections

#### Reflection Publisher-1

Answers:
1. We dont need to implement an interface inside BambangShop. The reasons are that the subscriber only observes the structure without any other subscribers with a diffrent implementation in the logic. The implementation of the subscriber itself is quite simple for now. Therefore, currently a single model struct is enough.

2. As of now, we're using Dashmap which is sufficient and necessary rather than using Vec. By using Dashmap, it enables us to do insertions and deletions more efficient. This can be explain since the id and url can be stored as keys in a key-value structure. As for their values, it would be the Subscriber annd the Program objects. 

3. Implementing a singleton pattern instead of DashMap wouldnt be enough to guarantee the safety for thread. Not guaranteing thread safety, makes it vulnerable when more than one threads try to modify the data. So by using DashMap, multiple threads are allowed to perfom operations  to the data altogether. In essence, DassMap is a thread safe data structure that we still need.

#### Reflection Publisher-2

Answers:

1. The reason why we need to seperate service and repository because both service and repository has diffrent functionality. This implementation follows the Single Responsibility Principle to improve maintainability and readability. Service handles the coordination of data operations by using the repository like the business logic. Meanwhile the Repository handles data that will be accessed and stored from the database itself. 

2. Just using the model would make itself, the model, quite complex. Bugs and errors would be more frequent than ever since maintaining it will be harder. If repository and service didnt got seperated from model, then the model has to handle a lot of functionally that was supposed to be the responsibility of repository and service.

3. To make sure the behaviour in each endpoints works as intended, i used Postman. Postman allows me to test specific endpoints from the project. It creates HTTP requests to the server with GET, POST, DELETE and many more. By doing so, the responses to the request are abled to be viewed.

#### Reflection Publisher-3
