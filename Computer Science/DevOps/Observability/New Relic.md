New Relic is an all-in-one cloud based observability solution. It provides visibility at every stage of the software lifecycle through a library of capabilities, and it also provides insights into: application performance, infrastructure health, user experience.

>[!info]
>An Observability Platform such as New Relic, can collect, store, manage, organize, curate, analyze and alert on data.

The New Relic observability platform uses agents to capture data from services (applications, hosts, databases) and send it back to the platform. 

Agents are integrated into a service through a process called **instrumentation**.

An agent is typically a file or few lines of code that automatically collects data on some service and sends it somewhere to be analyzed, such as an observability platform.
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

APM agent is a library that is added to the app runtime
The instrumentation is automatically, and the agent it's awhere of most of the comon frameworks. 
It also decorates the transaction with trace IDs, sot it can follow traces end to end and from the platform, capture loads of metrics directly from the app.

New Relic also captures each event, which is an transction that the applications executes.

Types of Agents:
- APM Agents --> it's for server-side application, for example, microservices. it lives rith  along side the aplication code, so it can get the maximum detail about the app. 
- Browser Agent --> for real time user experience, it's basically a line of javascript code that runs in the client browser. It can be placed manually or by the APM agent. Example: how long does it take to load the page.
- Mobile Agents --> also for user experience, it's addes to the app project before it's packaged. Anynone downloding the app will be sending telemetry data back to New Relic.
- Infrastructure agents --> runs on the host. it captures systems, processes, containers, storage and network status. It can intrument ilsefl at the sercie layer nad can collect telemetry data fro mthird party apps.

The New relic has integrartions with open source solutionsm like Prometheus and Istio. It is also an core participant in OpenTelemtry standards. 

APM stands for apllication perfofrmance monitroing, it enables developers to monitor adn troyble shoot the performance of the application in real time.

Infra monitoring allows DevOps teams to montor the health and performance of the service, contaienrs and cloud infra. It ncludes things like, tracking CPU and memory, network traffic and disk space utilization.

With Kubernetes and pixie, we can see detail information about the state of the cluster, nodes, pods . Pixie gives a deep visibility about the apps in the cluster by querin the kerneral directory using ibpf.

The infra gent comes with a log shiper, but it can integrate with other solution and display in test format along side with the entities they are related to it.

Entity --> anything that reports data to New Relic or contains data New Relic can has access to. 

Entities reporting data to New Relic are identity with an unique ID. For most entities the ID is incated by the attribute entitieGuid 

An entitie can be an individual data-reporting component, liek an application or a host, or a large group of them, such as workload.

New Relic keeps track of relantionship between entities

More insigth at the entity level helps the user to better monitor and troubleshiiting complex, modern systems.

The service map is a visual representation of the entire architec from front end do backend. it shows relationship between apps, databses, host, servers and web externals.
It works with distributed tracing, to connec relationship between entities.
users can filter teh service map by health statud, entity type or relation depth. 
As entering further at the network of entities, new relic will only display entities that are displaying issues. 

Distributed tracing --> tracks and observers sercies requests and transaatciosn as they flow trhow distribute systems. request can pass to vary inf areas to a service to reach completion. and when you can see the path other reeuqets across diferentes sercice you can easily pin point failura and perofrmance issues.

Grouoping entities in New Relci can be done by using Tags wich are key value pairs added to monitor entities, or to doashbold or workloads. It can be used as filters, when searching for an entity, or dashboard or workloads in the All entity page. Example: `team=ecommerce`.

workloads allows grouping entities in a logical way. A workloads can include any entity monitored in New Relic, dashboards and other workloads. teh created worklaod will become an entitie.




Entity Explorer

users can view each entity reporting in their account and its alert status at a glance, filter entites to find issues fast. 

the navigator option shows the system health at a glance trhou tviewing the alert status entities reporting to the account. The entities can be sorted by type, language, or agent version, or it can be sorted by health or name. 

the lookout provides a builtin view of entities that are drifting from normal behavior. The circle visualiotns in color are indicatiosn of severity and size. The default view provides insigths intro trhee keys service performance indicatiors: application trougput, reponse time and errors.

New relic analyzes these metrics to show how the data has behace durign the last five minutes compared to the prior hour.

pages view inscrsing is a good thing, beacause tha means more traffic to the website. 

The workload change tab helps to spot patterns in event attributes that might be related to the deviation in the main entity.

The related changes tab shows correlated behavior in the golden signals of related entities for a selected golden signal of the main entity.

The seasonality tab shows the changes in the selected golden signal over time and also surfaces any patterns in founded anomalies.

tags and Workloads
tags that are non-removable and that can be modified on the UI: agent version, language and accountID. They can only be modified by the source of the tag.
Tags can be used to filter entities, workloads and dashboards, tags can also be added to alert conditions and manage those.



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
##### <span style="color: #689d6a">Alerts</span>

New Relic allows the user to be informed abou issues for any entity or stream of telemetry data. Alerts can be defined based on metrics, Synthetic monitor and custom NRQL queries.

How to create alerts: 
1. Create 'Alert Condition' --> it defines the threshold for metrics
2. Group 'Alert Conditions' into an Alert Policy

When the Alert Condition is breached, the incidents are created. Incidents that need attention and action will end up becoming an issue

A group of issues are called 'Decisions' in New Relic.

Within every policy, workflows can be defined and those workflows decide to when and where to send notifications, which are sent to a Destination.

A Destination -->  notification channel. Example: email, slack or Pagerduty.

Applied intelligence is an engine in New Relic that tries to analyze the incidents, errors, logs and all that to understand the situation of your environment and let you be ahead of the problems.

all the alerts are basically based on queries.So as soon as one data point is above or below your threshold you won't get an incident. It has to be consistent.

If you have a runbook, which is basically a page on SharePoint or confluence or things like that that your system engineers can follow to resolve the problem

when you don't handle an issue or an incident, then after
a while a new one is created by default in your account, you can decide that incidents be sent to the email address that you use to sign up.


##### <span style="color: #689d6a">New Relic Query Language</span>

NQRL or the Newrelic query language is quite similar to a MySQL query language.
Newrelic also helps you with writing queries.

`SELECT average(duration) FROM Transaction` 

So most API calls and calls to web pages are web transaction types. And then there is a sub type that shows the technology behind that transaction.

So one thing we can do is to apply a Where statement for filtering, similar to a normal SQL statement.

```sql
SELECT average(duration) FROM Transaction WHERE transactionType in ('web', 'Web') AND transactionSubtType = 'Expressjs'
```

The query that we have written so far returned one single value.
One single value is useful for scenarios such as creating alert conditions.

grouping statement always comes before where statement. And in NQRL the grouping statement is called facet. And then after facet you mentioned that what field you want to use.

```sql
SELECT average(duration) FROM Transaction FACET transactionSubtType WHERE transaction in ('web', 'Web')
```

if you want to see the average, we can group the query result by different fields

```sql
SELECT average(duration) FROM Transaction FACET hosts WHERE transaction in ('web', 'Web')
```

```sql
SELECT average(duration), max(duration) FROM Transaction FACET hosts WHERE transaction in ('web', 'Web')
```

So how do we apply time limit?
There are two statements that we use to apply time limit. One of them is SINCE. 
The second statement that we use is until. Until, as you can imagine, is used for the end of the time period

```sql
SELECT average(duration) FROM Transaction FACET hosts WHERE transaction in ('web', 'Web') SINCE monday UNTIL today
```

So when in a New Relic dashboard, we change the time we are basically setting since and until for the query that is behind every graph.