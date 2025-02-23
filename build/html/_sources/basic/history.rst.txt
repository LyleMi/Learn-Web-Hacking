Web technology evolution
========================================

Simple website
----------------------------------------

Static page
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In the initial stage of Web technology, the main content of the website was static. Most sites were hosted on ISPs and composed of text and pictures. The production and expression form were also mainly based on tables. The behavior of users at that time was also very simple, basically just browsing the web.

Multimedia stage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
With the continuous development of technology, multimedia technologies such as audio, video, and Flash have been born. The addition of multimedia makes the web page more vivid and vivid, and the interaction on the web page also brings users a better experience.

CGI stage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Gradually, multimedia can no longer meet people's requests, so CGI (Common Gateway Interface) came into being. CGI defines the communication interface standard between the Web server and external applications, so the Web server can execute external programs through CGI, allowing external programs to generate dynamic content based on the content of the Web request.

At this time, various programming languages such as PHP/ASP/JSP have gradually joined the market, and more modular and more powerful applications can be realized based on these languages.

MVC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
As web application development becomes more and more standardized, ideas such as MVC have emerged. MVC is the abbreviation of Model/View/Control. Model is used to encapsulate data and data processing methods. View View is the HTML presentation of data. The controller Controller is responsible for responding to requests and coordinating Model and View.

The separation of Model, View and Controller is a typical idea of separation of concerns, which makes code reusability and organization better, and the configuration and flexibility of web applications are getting better and better. Data access has gradually replaced direct SQL access through an object-oriented method, and the concept of ORM (Object-Relational Mapping) emerged.

In addition to MVC, similar design ideas include MVP, MVVM, etc.

Data interaction
----------------------------------------

Simple data interaction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In the beginning of the development of web technology, most of the front-end and back-end interactions used relatively simple methods such as web forms, XML, SOAP, etc.

Ajax
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
At the beginning, the user can only get the results after submitting the entire form, which has a very poor user experience. As a result, Ajax (Asynchronous Javascript And XML) technology became popular, allowing applications to obtain or update data without updating the entire page. This makes web applications respond to user actions more quickly and avoids sending unchanged messages on the network.

RESTful
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
During the CGI period, front and back ends usually do not have strict distinctions. As the demand for decoupling and replication continues to increase, the concept of front and back ends begins to become clear. The front-end mainly refers to the website front-end part, which runs on the PC, mobile and other browsers to be displayed for users to browse. It consists of HTML5, CSS3, and JavaScript. The backend mainly refers to the logical part of the website, involving the addition, deletion, modification and search of data, etc.

At this time, REST (Representation State Transformation) gradually became a popular web architecture style.

REST encourages the organization of system functions based on URLs and make full use of the semantics of HTTP itself, rather than just using HTTP as a remote data transfer protocol. Generally, RESTful has the following characteristics:

- Domain name and main domain name are separated
- api.example.com
- example.com/api/
- With version control
- api.example.com/v1
- api.example.com/v2
- Locate resources using URL
- GET /users Get all users
- GET /team/:team/users Get all users of a team
- POST /users Create user
- PATCH/PUT /users Modify a user data
- DELETE /users Delete a user data
- Use HTTP verbs to describe operations
- GET Get resources, single or multiple
- POST Create Resources
- PUT/PATCH updates resources, the client provides complete resource data
- DELETE Delete Resources
- Use status code correctly
- Use status codes to improve readability of returned data
- Use JSON by default as the data response format
- There are clear documentation

GraphQL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The data in some network service scenarios has complex dependencies. In order to deal with these scenarios, Facebook launched GraphQL to query and store data in a graphical data structure. Some websites also use GraphQL as a way to interact with APIs.

Binary
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
As the business's performance requirements increase, the front and back ends have begun to use HTTP/2, custom Protocol Buffers and other methods to speed up data interaction.

Architecture evolution
----------------------------------------
As the business continues to develop, the business architecture is becoming more and more complex. Traditional functions are split into different modules, and concepts such as middleware and middle platforms have emerged. Technologies such as proxy services, load balancing, database subtables, off-site disaster recovery, caching, CDN, message queues, and security protection are becoming more and more widely used, increasing the complexity of Web development and operation and maintenance.

There are more and more client forms, and other scenarios such as iOS and Android are also appearing in the client scenarios of Web services.

The earlier relational databases MySQL, PostgreSQL, etc. can no longer meet the needs, and databases such as Redis/Memcached cache databases have emerged that meet specific needs.

In order to meet specific business needs, different infrastructures such as Lucene/Solr/Elasticsearch search application server, Kafka/RabbitMQ/ZeroMQ messaging system, Spark computing engine, and Hive data warehouse platform have emerged.

middleware
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Middleware is a standalone software program used to manage computing resources and network communications. Commonly used functions include filtering IP, merge interface, merge port, routing, permission verification, load balancing, reverse proxy, etc.

distributed
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
With the continuous increase in the amount of data, it is difficult for a single device to carry such access, and different functions are also split into different applications, thus a distributed service framework (RPC) that improves business reuse and integration has emerged.

Cloud Service
----------------------------------------
Before the birth of cloud computing, most of the computing resources were physical machines in a "bare metal" state. Operations and maintenance personnel chose the corresponding hardware, built the IDC network of the computer room, completed the provision of services, and invested in hardware infrastructure and maintenance. . After the cloud service appears, users can directly purchase cloud hosts, and the infrastructure is managed by suppliers. This method is also called IaaS (Infrastructure-as-a-Service).

As the architecture continues to develop, the application operation is more granular, the deployment environment is containerized, and various functions are disassembled into microservices or Serverless architectures.

Serverless
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The Serverless architecture consists of two parts, namely Faas (Function-as-a-Service) and BaaS (Backend-as-a-Service).

FaaS is an operation platform. Users upload logical functions that need to be executed, such as some timing tasks, data processing tasks, etc. to the cloud function platform, configure execution condition triggers, routing, etc., and the function execution can be completed through the cloud platform.

BaaS includes back-end service components, which complete third-party services based on APIs, mainly databases, object storage, message queues, log services, etc.

Microservices
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Microservices originated from the Micro-Web-Service proposed by Dr. Peter Rodgers at the Cloud Computing Expo in 2005. The fundamental idea is similar to Unix's pipeline design concept. In 2014, Martin Fowler and James Lewis jointly proposed the concept of microservices, defining the microservice architecture style as a method of developing a single application through a set of small services, each service running in its own process and through Lightweight mechanism for communication (HTTP API).

Microservices is a software architecture style applied to component design and deployment architecture. It combines complex large applications in a modular way:

- Each service function is cohesive and separates from the interface.
- Each service is highly autonomous and decoupled, and can be independently deployed, versioned and capacity scaled.
- Communication between services through API.
- Each service has an independent state and can only be accessed through the service itself.

With the continuous development of microservice technology, this idea has also been applied to the front end. In 2018, the first micro front-end tool single-spa appeared on github. Then a single-spa-based framework qiankun appeared.

API Gateway
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The API gateway is a server. The client only needs to use a simple access method to access the API gateway. The API gateway will proxy access to the back-end service. At the same time, because the service governance characteristics are uniformly placed on the API gateway, the service governance characteristics are changed. It can be transparent to the client, and to a certain extent, the basic characteristics such as service governance and business services are decoupled, and the upgrade of service governance characteristics is also easier to achieve.

Software Development
----------------------------------------

CI/CD
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Continuous Integration (CI) is the process of allowing developers to integrate their work into shared branches. Frequent integration helps resolve isolation, reducing the size of each commit to reduce the likelihood of merge conflicts.

Continuous Deployment (CD) is an extension of continuous integration that will build deployments from integrated test suites to pre-production environments. This allows it to evaluate each build directly in a production class environment, so developers can verify bug fixes or test new features without adding any effort.

Reference link
----------------------------------------
- `Scaling webapps for newbs <https://arcentry.com/blog/scaling-webapps-for-newbs-and-non-techies/>`_
- `GitHub's Restful HTTP API Design Decomposition <https://learnku.com/articles/24050>`_
