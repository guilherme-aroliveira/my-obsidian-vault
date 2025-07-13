New Relic is a full stack all-in-one cloud based observability platform. It provides insights into: application performance, infrastructure health, user experience.

>[!info]
>An Observability Platform such as New Relic, can collect, store, manage, organize, curate, analyze and alert on data.

Types of Agents:
- APM Agents --> stands for application performance monitoring, it's for server-side application, for example, microservices. 
- Browser Agent --> for browser applications, for example, for monitoring the metrics of a React website.
- Mobile Agents --> for monitoring the mobile applications that run on the customer's mobile handsets.
- Infrastructure agents --> for hosts
##### <span style="color: #689d6a">New Relic CLI</span>

New Relic CLI is required to install New Relic Agents, it can be used to send commands New Relic for example, to programmatic create new tags.

Multiple profiles can be created to configuring New Relic on the machine, every profile will have its own API KEY, its own license key, and its own account ID.

To create a new profile:

```shell
newrelic profiles add --profile Guilherme --apiKey [API] -r us
```

To select a profile:

```shell
newrelic profiles default --profile Guilherme
```

New Relic agent uses .NET providers to pull the metrics in `.dll` files
##### <span style="color: #689d6a">New Relic Platform</span>

Entity --> anything that sends data to New Relic or anything that contains data that New Relic can read and use. Example: a host server.

Every entity has a unique ID, which is in the format GUID (global unique identifies), to work with entities the unique ID is used. And entities, may have one or mote tags.

Tags --> key value pair. Example: a tag environment may have a value of staging. Only tags created by the user that can be deleted.

Entities can be grouped in workloads.

Workload --> a grouping of applications or services that are related to a specific business, function or purpose. Example: all used servers grouped into one workload.

Workloads enable you to manage and monitor the entities more efficiently.

To monitor a web application or a web page that runs in a browser using a browser agent. new relic provides all the necessary steps to configure the application, can even be a static web page. Distribute tracing option is useful to track application based on microservices. 

Now if we want to see that how this maps to the backend, you can click on distributed tracing.
A root entity is the highest level or layer that we have instrumented and we are monitoring.
Normally it's a web page or a mobile application
The default view in distributed tracing is root entity.

Apdex stands for Application Performance Index and its new Relic's way of understanding the performance of an application from the user's perspective.
It takes into account that how often users are satisfied with the performance, and how often users are dissatisfied with the performance.
Apdex is between 0 and 1, one is the best score, and zero is the worst score.
So the apdex is calculated as satisfied requests, plus half of tolerating requests divided by total number of requests.

So to set the correct Apdex, you need to go to application menu.

To see a problem within the code. 
part of my code is causing some threads to go into racing conditions, or if there is like an infinite loop or something that is not very optimized, then we cannot really see that in Newrelic unlesswe profile the code.
We can do profiling only for .Net Java, Python and Ruby applications only for these four

for Java, Python, and Ruby in the new relic config file you must have profile trace equal to true. Because profiling is not turned on by default
So in New Relic, if you go to a Python application or Java application, or DotNet or Ruby application.
You will have an item in the sub menu called Thread Profiler, and if I click on it, it will say that for how long you want to profile.
The longer you profile the more issues you will potentially pick up. But it just takes time.
##### <span style="color: #689d6a">New Relic Query Language</span>