Web technology evolution
========================================

simple website
----------------------------------------

static page
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In the initial stage of Web technology, the main content of the website was static. Most sites were hosted on ISPs and consisted of text and pictures. The production and presentation forms were mainly tables. User behavior at that time was also very simple, basically just browsing the web.

multimedia stage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
With the continuous development of technology, multimedia technologies such as audio, video, and Flash were born. The addition of multimedia makes web pages more vivid, and the interactions on web pages also bring a better experience to users.

CGI stage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Gradually, multimedia can no longer meet people's requests, so CGI (Common Gateway Interface) came into being. CGI defines the communication interface standard between the Web server and external applications, so the Web server can execute external programs through CGI, allowing the external programs to generate dynamic content based on the Web request content.

At this time, various programming languages ​​such as PHP/ASP/JSP are gradually joining the market. Based on these languages, more modular and powerful applications can be implemented.

MVC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
As Web application development becomes more and more standardized, ideas such as MVC have emerged. MVC is the abbreviation of Model/View/Control. Model is used to encapsulate data and data processing methods. View is the HTML display of data. Controller is responsible for responding to requests and coordinating Model and View.

The separation of Model, View and Controller is a typical idea of ​​separation of concerns, which makes code reusability and organization better, and the configurability and flexibility of Web applications are getting better and better. Data access has gradually replaced direct SQL access through object-oriented methods, and the concept of ORM (Object-Relational Mapping) has emerged.

In addition to MVC, similar design ideas include MVP, MVVM, etc.

Data interaction
----------------------------------------

Simple data interaction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
At the beginning of the development of Web technology, most front-end and back-end interactions used simpler methods such as Web forms, XML, and SOAP.

Ajax
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
At the beginning, users could only get the results after submitting the entire form, which resulted in a very poor user experience. As a result, Ajax (Asynchronous Javascript And XML) technology gradually became popular, which allows applications to obtain or update data without updating the entire page. This allows web applications to respond more quickly to user actions and avoids sending unchanged information over the network.

RESTful
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In the CGI era, there was usually no strict distinction between front-end and back-end. As the demand for decoupling and integration continues to increase, the concepts of front-end and back-end begin to become clear. The front-end mainly refers to the front-end part of the website, which runs on PC, mobile and other browsers and displays web pages for users to browse. It is composed of HTML5, CSS3, and JavaScript. The backend mainly refers to the logical part of the website, involving the addition, deletion, modification and query of data.

At this time, REST (Representation State Transformation) gradually became a popular Web architecture style.

REST encourages organizing system functions based on URLs and making full use of the semantics of HTTP itself, rather than just using HTTP as a remote data transmission protocol. Generally RESTful has the following characteristics:

- Separate domain name and main domain name
    - api.example.com
    - example.com/api/
- Comes with version control
    - api.example.com/v1
    - api.example.com/v2
- Locate resources using URLs
    - GET /users gets all users
    - GET /team/:team/users Get all users of a team
    - POST /users to create users
    - PATCH/PUT /users Modify a user's data
    - DELETE /users deletes user data
- Use HTTP verbs to describe operations
    - GET gets resources, single or multiple
    - POST creates resources
    - PUT/PATCH updates resources, and the client provides complete resource data
    - DELETE deletes resources
- Use status codes correctly
    - Use status codes to improve the readability of returned data
- Use JSON as data response format by default
- Have clear documentation

GraphQL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The data in some network service scenarios has complex dependencies. In order to deal with these scenarios, Facebook launched GraphQL to query and store data in a graph-like data structure. Some websites also use GraphQL as a way to interact with APIs.

binary
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
As business requirements for performance increase, the front and back ends begin to use HTTP/2, custom Protocol Buffer and other methods to speed up data interaction.

Architecture evolution
----------------------------------------
As business continues to develop, business architecture becomes more and more complex. Traditional functions were split into different modules, and concepts such as middleware and middle platform emerged. Technologies such as proxy services, load balancing, database sharding, remote disaster recovery, caching, CDN, message queues, and security protection are increasingly widely used, increasing the complexity of Web development and operation and maintenance.

There are more and more forms of clients. In addition to the Web, other scenarios such as iOS and Android also appear in client scenarios of Web services.

The earlier relational databases MySQL, PostgreSQL, etc. can no longer meet the needs, and a class of databases such as Redis/Memcached cache database have emerged to meet specific needs.

In order to meet specific business needs, different infrastructures such as Lucene/Solr/Elasticsearch search application server, Kafka/RabbitMQ/ZeroMQ messaging system, Spark computing engine, and Hive data warehouse platform have emerged.

middleware
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Middleware is an independent software program that manages computing resources and network communications. Commonly used functions include IP filtering, interface merging, port merging, routing, permission verification, load balancing, reverse proxy, etc.

distributed
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
As the amount of data continues to increase, it is difficult for a single device to carry such access, and different functions are split into different applications. Therefore, a distributed service framework (RPC) has emerged to improve business reuse and integration.

cloud services
----------------------------------------
Before the birth of cloud computing, most computing resources were physical machines in a "bare metal" state. Operation and maintenance personnel selected hardware with corresponding specifications, built an IDC network in the computer room, and completed service provision. The cost of investing in hardware infrastructure construction and maintenance was very high. After the emergence of cloud services, users can directly purchase cloud hosts, and the infrastructure is managed by the provider. This approach is also called IaaS (Infrastructure-as-a-Service).

As the architecture continues to develop, application operation becomes more fine-grained, the deployment environment is containerized, and each function is split into microservices or serverless architecture.

Serverless
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Serverless architecture consists of two parts, namely Faas (Function-as-a-Service) and BaaS (Backend-as-a-Service).

FaaS is an operating platform. Users upload logical functions that need to be executed, such as some scheduled tasks, data processing tasks, etc. to the cloud function platform, configure execution condition triggers, routing, etc., and then the function execution can be completed through the cloud platform.

BaaS includes back-end service components, which implement third-party services based on APIs, mainly databases, object storage, message queues, log services, etc.

microservices
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Microservices originated from the Micro-Web-Service proposed by Dr. Peter Rodgers at the Cloud Computing Expo in 2005. The basic idea is similar to the Unix pipeline design concept. In 2014, Martin Fowler and James Lewis jointly proposed the concept of microservices, defining the microservices architectural style as a method of developing a single application through a set of small services. Each service runs in its own process and communicates through a lightweight mechanism (HTTP API).

Microservices is a software architectural style applied to component design and deployment architecture. It uses a modular approach to compose complex large-scale applications:

- Each service function is cohesive and implementation is separated from the interface.
- Each service is highly autonomous and decoupled from each other, allowing independent deployment, version control, and capacity scaling.
- Communicate between various services through API.
- Each service has independent state and can only be accessed through the service itself.

With the continuous development of microservice technology, this idea has also been applied to the front end. In 2018, the first micro front-end tool single-spa appeared on github. Then the framework qiankun based on single-spa appeared.

API gateway
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The API gateway is a server. The client only needs to use a simple access method to access the API gateway in a unified manner. The API gateway will proxy access to the back-end services. At the same time, because the service governance features are unified on the API gateway, changes in the service governance features can be transparent to the client. To a certain extent, the decoupling of basic features such as service governance and business services is achieved, and the upgrade of service governance features is also relatively easy to implement.

software development
----------------------------------------

CI/CD
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Continuous Integration (CI) is the process of letting developers integrate work into shared branches. Frequent integrations help resolve isolation and reduce the size of each commit to reduce the likelihood of merge conflicts.

Continuous Deployment (CD) is an extension of continuous integration that deploys builds from an integration test suite to a pre-production environment. This allows it to evaluate each build directly in a production-like environment, so developers can verify bug fixes or test new features without any added effort.

Reference link
----------------------------------------
- `Scaling webapps for newbs <https://arcentry.com/blog/scaling-webapps-for-newbs-and-non-techies/>`_
- `GitHub’s Restful HTTP API design breakdown <https://learnku.com/articles/24050>`_
