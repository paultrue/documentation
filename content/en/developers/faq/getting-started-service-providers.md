## Introduction

Datadog provides insights into your clients' hybrid cloud infrastructures and applications. With our intuitive UI and powerful API, you can onboard, provision, and manage your clients' diverse environments, while establishing data security in each account.

We want you to start monitoring your clients' environments quickly and efficiently, so we've highlighted best practices in this document. We divided this document into four main sections:

- [Laying the Groundwork](#laying-the-groundwork): Contains information about how to get started and which key decisions you should make at the very beginning.
- [Data Intake](#data-intake-getting-data-to-datadog): Explains how data can be fed into Datadog and which prerequisites need to be met in your or your clients' environments.
- [Delivering Value](#delivering-value): Walks through recommended steps once you have data flowing into Datadog.
- [Up & Running](#up--running): Covers how to stay up to date with the Datadog platform. Should you have any questions or feedback about any of these best practices, please reach out to your Partner Account Manager.

## Key considerations for MSPs

The way you as a service provider get started with Datadog depends on your business model and your operational model:

- **Business model**: A key question to answer is whether you are planning on giving your clients their own access to Datadog or not. If you do choose to give clients access to Datadog, you will then likely need to set up a multi-organization account (more on that below) to keep client data separate and private.
- **Operational model**: Another key consideration is whether your client base consists of many homogeneous clients —where programmatic management of many similar-looking Datadog organisations will be more important —or whether your clients are fewer or more heterogeneous.

## Laying the groundwork

### Prerequisites

Before working on implementing Datadog as a Service Provider, it is recommended that you complete the [Datadog Technical Specialist training][1] available exclusively for Datadog partners.

Completing the training and the certification will familiarize you with many of the topics covered in the next chapters, enabling you to get started immediately.

### Organization setup

One of the key decisions for a Service Provider to make is how to set up client Datadog accounts, called "Organizations" (or "orgs" for short). While users can be associated with more than one organization, monitored resources are tied to a single organization. Choosing the right organization structure from the beginning will help you more quickly create value for you and your clients.

#### Single-organization or multiple-organization

Datadog offers the possibility of managing multiple child organizations from one parent organization. This is the typical deployment model used by Managed Service Providers that have clients which should not have access to each others' data. In a multi-org set up, one child organization is created for each client, and the client is restricted to their own child organization. If you have no plans to give your clients access to Datadog and therefore do not have a strict requirement to separate client data, a single-org setup would suffice.

For more information about Organization Management, see the [Managing Multiple Organization Accounts][2] documentation.

#### Separate orgs for dev, test and production?

A common question from MSP partners is whether separate Datadog orgs should be set up to manage development, test, and production resources in either your or your clients' environments.

Datadog does not recommend separating development, test, and production resources from the rest of the resources. The recommended approach is to manage all resources in the same Datadog organization and delineate the environments through tags. For more information, see [Tagging strategy](#tagging-strategy). 

### Custom subdomains

We encourage our MSP partners to make use of the custom subdomain feature to improve their Datadog experience when handling a large number of organizations.

By default, any Datadog organization is accessed through Datadog's access pages, [https://app.datadoghq.com](https://app.datadoghq.com) and [https://app.datadoghq.eu](https://app.datadoghq.eu). However, custom subdomains can provide a unique URL for each sub-organization. For example, `https://account-a.datadoghq.com`. For more information, see [Custom sub-domains](https://docs.datadoghq.com/account_management/multi_organization/#custom-sub-domains).

### User roles and custom role-based access control (RBAC)

Experience shows that both MSP-internal as well as client users will often not fall clearly into one of the three [Datadog default roles][3] that Datadog provides out of the box. It is therefore good practice to create [Custom roles][4] to limit user permissions in certain areas, such as:
- The ability to manage monitors, which can possibly generate a large volume of notifications.
- The ability to change log management configurations, which can have a cost impact.

### Single sign-on (SSO) considerations

In a service provider context, you have two considerations for Single sign-on (SSO):
- Single sign-on for your organization
- Single sign-on for your clients

Besides the obvious advantage of a unified authentication mechanism, using SAML Single Sign-On also vastly simplifies the user provisioning process. Using SAML allows you to use Just-in-Time (JiT) user provisioning, eliminating the need to manually or programmatically create users.

Please note that SAML authentication is enabled on a Datadog organization or sub-org, meaning you can have different SAML providers for different sub-orgs. However, this also means that if you have two groups of users with different SAML providers, those users will have to be in separate orgs. Should you plan on using different SAML authentication providers for different groups of users, make sure to take this into consideration when planning your multi-organization setup.

For information, see:
- [Set up SAML][5] for multiple-organization accounts
- [Single sign-on with SAML][6]

### Adding Users

#### User creation

Datadog offers multiple ways to quickly provision users for their respective organizations:

- [Add batches of users via the UI][7] 
- [Create users through the API][8]
- Use an authentication service like SAML together with [Just-in-Time (JiT) provisioning][9]

#### User training

Datadog's mantra is "Simple, but not simplistic," meaning that our goal is to provide a service that is easy and intuitive to use. Experience shows that most users feel comfortable working with the product, and learning as they go along.

For users that prefer to have training on the most important aspects of the product, Datadog provides various ways for users to familiarize themselves with the product:

- [Datadog's YouTube channel][10]: With introduction videos posted whenever new features are released as well as videos on Tips & Tricks and Best Practices, Datadog's YouTube channel is a great source for high-level training.
- [Datadog Learning Center][11]: The Datadog Learning Center is a great way for users to get to know the platform in-depth. When signing up for the Learning Center, a Datadog sandbox environment is automatically provisioned free of charge, allowing users to play around with the product without fear of breaking anything.
- [The Datadog Blog][12]: With over 700 entries, The blog is a key source of information on how to use Datadog to monitor key services, tools, and technologies in your client environments, as well as information on the latest product releases.
- [Datadog Partner Network (DPN) Enablement Center][13]: Through the DPN, Datadog service provider partners have access to a series of video courses for service provider salespeople and technical professionals.

Should you as a service provider plan on building your own training material for your clients and have any recommendations on what content would be helpful for you, please reach out to your Datadog partner representative.

## Data intake

Now that we have laid down the foundation, it is time to start getting data into Datadog. Initially, the objective of this phase should be to gather data to provide immediate value to you or your clients. However, in the long run you should consider this an ongoing process where you constantly assess changes to your environment, such as:

- New technologies employed by your organization or your clients
- New processes are introduced
- New product features of Datadog Any of these changes should be considered regularly to ensure that all necessary telemetry is being ingested into Datadog. Datadog offers several different ways to collect data:
- Cloud service integrations (out of the box)
- The Datadog Agent & Agent-based Integrations (out of the box)
- APIs / Library Integrations & Custom Checks We cover each ingestion method below. You can watch a brief introduction into all three categories in the video Datadog 101 - Collection.

### Integrations

One way to provide immediate value to your clients is through integrations. Datadog offers {{< translate key="integration_count" >}} integrations that collect metrics and logs from a wide array of technologies. Some integrations rely on installing the Datadog Agent software, others are authentication-based and rely on the Datadog API, and some collect data based on the language that an application is written in.

For more information on integrations and the Datadog Agent, see:
- [Introduction to Integrations][14]
- [List of Datadog Integrations][17]
- [The Datadog Agent][15]
- [Getting Started with the Agent][16]

### APIs / Library Integrations & Custom Checks

With scalability and extensibility as our main objectives, Datadog offers a number of APIs and SDKs to extend the platform in situations where:
- Installing the Agent might not be possible due to security or other restrictions, for example on IoT devices.
- The capabilities of the Datadog Agent and its integrations do not cover a technology or requirement.

In these cases, using APIs enables you to capture relevant telemetry into the observability platform for your clients.

We can distinguish between three key API areas that would be of most interest to you as a service provider:
- Public APIs for data ingestion
- Custom checks
- Local APIs for data ingestion on the Agent

#### Public APIs for data ingestion

In cases where using cloud service integrations or the Agent is not possible or desired, the following APIs can be helpful for data intake:

- Logs can be forwarded directly to Datadog's [log ingestion endpoint][18].
- Metrics can be forwarded directly to Datadog's [metrics API][19].
- Events can be forwarded directly to Datadog's [events API][20].
- Traces can be forwarded directly to Datadog's [trace/span API][21].

#### Custom checks

While Datadog offers {{< translate key="integration_count" >}} integrations, there might be cases where your client runs a custom application that cannot be covered with any of the existing integrations. For your clients to monitor these applications with Datadog, the Datadog Agent has the ability to execute custom checks.

For more information, see [Custom Checks][22].

#### Local APIs for data ingestion on the Agent

There might be situations where metrics or events are not captured by any of the Datadog Agent integrations and, in addition, writing a custom check is not an option as the source of the application might only be running sporadically. This often applies to simple jobs such as cron jobs, which do not have their own log files, but should still be able to send status information (events) and metrics to the observability platform.

The Datadog Agent comes bundled with DogStatsD, a metrics aggregation service, which accepts data via UDP, enabling you to:
- [Submit Events][23]
- [Submit Custom Metrics][24]

Besides using the endpoints directly, Datadog also offers client libraries to facilitate the submission of metrics and events to DogStatsD. 

For more information, see:
- [Libraries][25]
- [API Reference][26]

### Tagging strategy

Now that you have learned about the different ways of getting data into Datadog, we need to cover one important step to make sure that you and your clients will be able to benefit from all of Datadog's features: Tagging.

Tags are labels that are attached to your data (hosts, containers, events, traces, logs, metrics, etc.) that enable you to filter, group, and correlate your data throughout Datadog. Tagging binds different telemetry types in Datadog, allowing for correlation and call to action between metrics, traces, and logs. This is accomplished with reserved tag keys. Here are some examples:

Setting a consistent tagging strategy upfront will pave the way to a successful Datadog implementation for you as a service provider and ultimately increase value realization for your clients.

When thinking about tagging, take into consideration the following factors:

- Technology: This allows the comparison of the same technology between teams/clients.
- Environment: This allows the comparison of the performance between test, production, and other environments.
- Location: This will be helpful to understand issues that are related to specific data centers or cloud service provider availability zones.
- Business Service: This enables you and your clients to easily filter all building blocks of a business service, regardless of technology.
- Role: This enables users to understand which role the entity plays in a business service.
- Responsibility: This will enable both the responsible team to easily filter all of their resources as well as enable other users and teams to quickly identify which team is responsible for a certain service.

Please consult the following tagging resources:

- [Getting Started with Tags][27]
- [Best practices for tagging your infrastructure and applications][28] (Blog)
- [Tagging Best Practices][29] (Training)

Tagging strategy: 
- [Unified Service Tagging][30]
- [Kubernetes Tag Extraction][31]
- [AWS Tagging][32] (AWS Documentation)
- [Serverless Tagging][33]
- [Live Container Tagging][34]

### Agent rollout

As we've seen in the previous sections, there are many benefits to using the Datadog Agent for data collection. Below we'll cover four phases of Agent rollout:

- Prerequisites for Agent deployment
- Initial Agent deployment to the existing infrastructure
- Provisioning of new infrastructure
- Monitoring the continuous provisioning processes

#### Prerequisites for Agent deployment

Depending on the platform and operating system, there might be different prerequisites for the Agent. See [the official Agent documentation][35] to familiarize yourself with those requirements.

The main prerequisite for the Agent on any platform is network connectivity. Traffic is always initiated by the Agent to Datadog. No sessions are ever initiated from Datadog back to the Agent. Except in rare cases, inbound connectivity (limited through local firewalls) is not a factor for Agent deployments.

To work properly, the Agent requires the ability to send traffic to the Datadog service over SSL via 443/tcp. For a full list of ports ports used by the agent, see [Network Traffic][36].

In some circumstances, Agent version-specific endpoints can cause maintenance problems, in which case we can provide a version-agnostic endpoint. If you need a version-agnostic endpoint, contact Datadog support.

##### Agent proxy

In many client environments, opening direct connectivity from the Agent to Datadog is not possible or desired. To enable connectivity, Datadog offers a few different options to proxy the Agent traffic.

For more information, see [Agent Proxy Configuration][37].

#### Agent deployment, upgrade, and configuration

There are various ways to deploy the Datadog Agent to your own and your client's infrastructure. As most service providers already have some configuration management tool in place, it is good practice to use the existing tool for Agent rollout.

Here are some examples of how to manage your Datadog Agent estate with configuration management tools:
- [Deploying Datadog Agents with Chef][38] (Blog)
- [Puppet + Datadog: Automate + monitor your systems][39] (Blog)
- [Deploying and Configuring Datadog with CloudFormation][40] (Blog)
- [How to Use Ansible to Automate Datadog Configuration][41] (Video)
- [How to deploy the Datadog agent on AWS hosts with Ansible dynamic inventories][42] (Blog)

If you don't plan on using Datadog's repositories, you can always find the latest Agent releases in the [public Github repository][43]. It is recommended that you [verify the distribution channel][44] of Agent packages before deployment.

#### Monitoring the continuous provisioning processes

While it is good practice to not only use configuration management tools for deploying Datadog, we also recommend leveraging Datadog to monitor proper operation of the tools. Here are some examples:

- [Ask your systems what's going on: monitor Chef with Datadog][45] (Blog)
- [Ansible + Datadog: Monitor your automation, automate your monitoring][46] (Blog)

## Delivering value

After you've set up data ingestion, you can take several additional steps to maximize the value for your clients. Below, we cover the following key areas to focus on:

- [Setting up Monitors and Downtimes](#setting-up-monitors-and-downtimes)
- [Setting up Visualizations and Dashboards](#setting-up-visualizations-with-dashboards)
- [Setting up Service Level Objectives](#setting-up-service-level-objectives-slos)
- [Using Watchdog](#using-watchdog)

### Setting up monitors and downtimes

Monitors and alerts draw human attention to particular systems and services that require inspection and intervention. To generate alerts, Datadog offers:

- Monitors - the definitions for alert conditions
- Downtimes - time periods when alerts should be raised or suppressed

To familiarize yourself with the concept of Monitors in general, we recommend the following resources:
- [Monitoring 101 - Alerting on what matters][47] (blog).
- [Intro to Monitoring][48] (Training).

#### Thoughts about monitor migrations

A frequent situation service providers can find themselves in is migrating a client from a different monitoring or observability platform to Datadog. In such cases, it might seem logical to simply replicate any monitor from the previous solution to Datadog. However, experience shows that with this approach many of Datadog's features that improve issue detection and resolution times or reduce alert fatigue will remain unused.

We therefore recommend that as part of such a migration project, existing alert/threshold definitions should be reviewed to answer if:

- The metric has a time-based variation, in which case [an Anomaly Monitor][49] might be a better approach.
- The metric has a load-based variation, in which case an [arithmetic monitor][50] might be the best approach by combining a metric with a load- indicating metric (i.e., load on the systems might be higher if there are more users using a service).
- The absolute value of the metric is less important than the rate of change, in which case a [change monitor][51] or a [forecast monitor][52] might be the best approach.
- The value of the metric itself is less important than whether it is different from the value for other hosts or entities (i.e., one node in a cluster is experiencing high latency where other nodes are not), in which case the [outlier monitor][53] is the best approach.
- Only the combination of multiple metrics present an actionable situation, in which case [composite monitors][54] offer an easy way without any scripting needed.

#### Programmatic monitor management

As a service provider, management of possibly very large amounts of monitors for you and your clients is best accomplished programmatically through one of the following ways:

- [Datadog Monitors API][55]
- Terraform
  - [How to Manage Datadog Resources Using Terraform][56] (Video)
  - [Automate Monitoring with the Terraform Datadog Provider][57] (HashiCorp Tutorial)

We also recommend that you [tag monitors][58] to make the management of large numbers of monitors easier.

#### Recommended monitors

While creating monitors for technologies that you manage on a daily basis might be straightforward, chances are that you will run into technologies your clients operate that you as the service provider might not have a lot of experience with. It's for situations like these that Datadog offers [Recommended Monitors][59] to help you onboard new technologies quickly and confidently.

To find out more about Monitors, see:
- [Manage Monitors][60]
- [Monitors][61]
- [Creating Dynamic Alerts Using Tag Values][62] (Video)
- [Why Did My Monitor Settings Change Not Take Effect?][63] (FAQ)

#### Downtimes

A common problem with monitors and alerts is alert fatigue, where an overabundance of alarms or notifications causes desensitization to the alarms. One way to combat alert fatigue is to limit the number of false positive alarms, especially in controlled situations such as planned system shutdowns, maintenance, or upgrade-windows.

Datadog's Downtimes offer you and your clients a way to mute monitors during times of planned (or ad hoc) maintenance.

To find out more about managing downtimes, especially programmatically, see:
- [Downtime][64]
- [Mute Datadog Alerts for Planned Downtimes][65] (Blog)
- [Managing Datadog with Terraform][66] (Blog)
- [Downtime API][67]
- [Prevent alerts from Monitors that were in downtime][68]

#### Notifications

Some general guidelines for notifications:
- Alert liberally; page judiciously
- Page on symptoms, rather than causes

Datadog offers various channels through which you or your clients can notify users about important alerts:

- Email notifications
- Integrations, such as:
  - [Slack][69]
  - [PagerDuty][70]
  - [Flowdock][71]
  - [ServiceNow][72]
  - [Google Hangouts Chat][73]
  - [Microsoft Teams][74]
  - And [many more][75]

You can also invoke any REST API using the generic [Webhooks integration][76], which can be used not only to notify users but also to trigger automatic remediation workflows.

To find out more about Notifications, see:

- [Notifications][77]
- [Send SMS Alerts with Webhooks and Twilio][78] (Blog)

### Setting up visualizations with Dashboards 

Visualizations are a great way to give your clients a clear picture of complex tech stacks and abundance of metrics and events being collected. Dashboards are a natural starting point to investigate a potential issue you or your client was notified about by a monitor.

#### Out-of-the-box dashboards

The moment that an Agent or Cloud Integration is set up, Datadog automatically enables out-of-the-box dashboards for the newly integrated service or technology, providing immediate insights. Out-of-the-box dashboards can also be cloned, giving you a great starting point for a custom dashboard.

#### Building custom dashboards

By not only offering a technology-centric perspective to your clients but also a business-centric perspective, tailored to different personas, you as a service provider can provide extra value and distinguish yourself from your competitors.

There are a number of dashboard best practices we recommend you take into consideration when building your dashboards:

- Focus on work metrics rather than too many resource metrics. To understand the difference, see [Monitoring 101: Collecting the right data][79] (blog).
- Make use of [event overlays][80] to correlate metrics and events.
- Annotate the dashboards with [free text information][81] on what data is shown and what to do in case the dashboard indicates an issue.

To find out more about Dashboards, see:
- [Building Better Dashboards][82] (Training)
- Use the [Datadog Notebooks][83] feature to gather data in an exploratory fashion and draft dashboards
- [Monitor Datacenters and Networks with Datadog][84] (Blog)
- [Use Associated Template Variables][85] (Blog)
- [The Datadog Dashboard API][86]
- [Configure Observability as Code with Terraform & Datadog][87] (HashiCorp webinar)

#### Visualizations for users without Datadog access

Depending on your business model, your clients might not require access to Datadog themselves but you might still want to provide Datadog visualizations to your clients. To do this, you have the following options:
- [Dashboard sharing][88]: Share a read-only dashboard via public URL to provide a status page to your clients or share it privately using an individual e-mail address.
  - As a service provider, your business needs to be able to scale. Therefore [managing shared dashboards via our APIs][89] will probably be the most efficient approach.
- Embeddable graphs: If you have a client portal in which you want to present Datadog information, Embeddable Graphs are the way to go. By using parameters, you can filter data according to your needs. 
  For more information, see:
  - [Embeddable Graphs API][90]
  - [Embeddable Graphs with Template Variables][91]


#### Setting up Service Level Objectives (SLOs)

As a service provider it is a good idea to continually present the quality and level of your services to your clients in a transparent way. Service Level Objectives (SLOs) are a great way to monitor and visualize the service quality on behalf of your clients, and also help your clients implement service level-based reporting internally.

The following material might be helpful for you when setting up and managing SLOs:
- To get started, we recommend [Service Level Objectives 101: Establishing Effective SLOs][92] (Blog). 
- [SLO Checklist][93]
- [Best practices for managing your SLOs with Datadog][94] (Blog)
- [Track the status of all your SLOs in Datadog][95] (Blog)
- [The Datadog SLO API][96]

### Using Watchdog

Watchdog is an algorithmic feature that automatically detects potential application and infrastructure issues.

We recommend that you set up a Watchdog Monitor for your own staff or your client with a notification whenever Watchdog has detected a new irregularity.

For more information, see [Watchdog][97]

## Up & Running

In this chapter we cover how to monitor both individual client and aggregate usage of the Datadog platform, and stay up to date with Datadog.

### Billing & Usage Reporting

Note: The details in this section apply to a Multi-Organization account setup

With a Datadog admin role in the parent organization you can view the total and billable usage of all your organizations (both child and parent) as well as how your clients' usage has changed over the past six months as explained here.

Usage is aggregated across all child organizations and billed at the parent organization level. From the parent organization, those with an admin role can view aggregate usage across all child organizations as well as drill into usage of individual child organizations.

In case existing roles are not flexible enough for you or your client organization, you can create new custom roles. With custom roles, in addition to the general permissions, it is possible to define more granular permissions for specific assets or data types. You can find the list of permissions specific to billing and usage assets here.

In addition to the usage page, below you will find a number of additional resources which might help you as a service provider estimate and manage clients' usage as well as provide easy allocations and chargebacks:

- Estimated Usage Metrics: Datadog calculates your clients' current estimated usage in near real-time. Estimated usage metrics enable you to graph your estimated usage, create monitors or alerts around your estimated usage based on thresholds of your choosing and get instant alerts on spikes or drops in your usage.

- Shared Dashboards: Shared dashboards and graphs allow you to display metric, trace, and log visualizations with your users outside of Datadog. You can publish estimated usage metrics dashboards for your clients to track.

- Usage Attribution: The Usage Attribution page provides: lists to the existing tag keys that usage is being broken down by and provides the ability to change and add new ones; generates daily .tsv (tab separated values) files for most usage types; and summarizes usage at the end of each month not only by child-organizations but also by tag. Please note that usage attribution is an advanced feature included in the Enterprise plan. For all other plans, contact your Datadog partner representative to request this feature.

### Staying up to date with Datadog

### Learn about new features

There are multiple ways you can stay up to date with Datadog. The most common and easy way is to look at the release notes page in the Datadog user interface:

As a Datadog Partner Network member, you also have exclusive access to the following material:

- Collateral and training material in the Datadog Partner Network portal.
- Quarterly DPN Live Briefing Webinar: watch for the invite in your inbox or watch the recorded sessions.

### Learn with Datadog

In the process of building a monitoring and analytics platform that ingests trillions of data points a day, Datadog has learned many lessons about scalable, distributed systems in the cloud. We like to share those experiences with our community in our "Datadog on..." series.

We recommend you subscribe to it at: https://datadogon.datadoghq.com/

### Status information

Datadog provides the following resources for you to get up-to-date status information on service status:

- US region: https://status.datadoghq.com
- EU region: https://status.datadoghq.eu

We recommend that you subscribe to this page to receive notifications about status changes.

If you would like to see the status of third party integrations you might have enabled with Datadog, check out: https://datadogintegrations. statuspage.io

### Other resources

Last but not least, feel free to explore other important resources to stay up to date with Datadog:

- Github repositories:
  - https://github.com/DataDog/datadog-agent
  - https://github.com/DataDog/integrations-core
  - https://github.com/DataDog/integrations-extras/
  - https://github.com/DataDog/Miscellany
- Datadog blog: https://www.datadoghq.com/blog/
- LinkedIn: https://www.linkedin.com/company/datadog/
- Twitter: https://twitter.com/datadoghq
- Facebook: https://www.facebook.com/datadoghq/
- YouTube: https://www.youtube.com/user/DatadogHQ
  - Tips and Tricks channel
- Dash Conferences:
  - Dash 2019
  - Dash 2020

[1]: https://partners.datadoghq.com/prm/English/c/technical_content
[2]: /account_management/multi_organization/
[3]: /account_management/rbac/?tab=datadogapplication#datadog-default-roles
[4]: /account_management/rbac/?tab=datadogapplication#custom-roles
[5]: /account_management/multi_organization/#set-up-saml
[6]: /account_management/saml/
[7]: /account_management/users/#add-new-members-and-manage-invites
[8]: /api/latest/users/#create-a-user
[9]: /account_management/saml/#just-in-time-jit-provisioning
[10]: https://www.youtube.com/user/DatadogHQ
[11]: https://learn.datadoghq.com/
[12]: https://www.datadoghq.com/blog/
[13]: https://partners.datadoghq.com/
[14]: /getting_started/integrations/
[15]: /agent/
[16]: /getting_started/agent/
[17]: /integrations/
[18]: /getting_started/logs
[19]: /api/latest/metrics
[20]: /api/latest/events
[21]: /api/latest/tracing/
[22]: /developers/custom_checks/
[23]: /events/guides/dogstatsd/ 
[24]: /metrics/custom_metrics/
[25]: /developers/community/libraries/#api-and-dogstatsd-client-libraries
[26]: /api/latest/
[27]: /getting_started/tagging/
[28]: https://www.datadoghq.com/blog/tagging-best-practices/
[29]: https://learn.datadoghq.com/courses/tagging-best-practices
[30]: /getting_started/tagging/unified_service_tagging?tab=kubernetes
[31]: /agent/kubernetes/tag/
[32]: https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html
[33]: /serverless/serverless_tagging/?tab=serverlessframework#overview
[34]: /infrastructure/livecontainers
[35]: /agent/basic_agent_usage/
[36]: /agent/guide/network/
[37]: /agent/proxy/
[38]: https://www.datadoghq.com/blog/deploying-datadog-with-chef-roles/
[40]: https://www.datadoghq.com/blog/monitor-puppet-datadog/
[41]: https://www.datadoghq.com/blog/deploying-datadog-with-cloudformation/
[42]: https://www.youtube.com/watch?v=EYoqwiXFrlQ
[42]: https://www.datadoghq.com/blog/install-datadog-with-ansible-dynamic-inventories/
[43]: https://github.com/DataDog/datadog-agent/releases
[44]: /data_security/agent/#agent-distribution
[45]: https://www.datadoghq.com/blog/monitor-chef-with-datadog/
[46]: https://www.datadoghq.com/blog/ansible-datadog-monitor-your-automation-automate-your-monitoring/
[47]: https://www.datadoghq.com/blog/monitoring-101-alerting/
[48]: https://learn.datadoghq.com/courses/intro-to-monitoring
[49]: /monitors/create/types/anomaly/
[50]: /monitors/guide/monitor-arithmetic-and-sparse-metrics/
[51]: /monitors/create/types/metric/?tab=change
[52]: /monitors/create/types/forecasts/?tab=linear
[53]: /monitors/create/types/outlier/?tab=dbscan
[54]: /monitors/create/types/composite/
[55]: /api/latest/monitors/
[56]: https://www.youtube.com/watch?v=Ell_kU4gEGI
[57]: https://learn.hashicorp.com/tutorials/terraform/datadog-provider
[58]: https://www.datadoghq.com/blog/tagging-best-practices-monitors/
[59]: https://www.datadoghq.com/blog/datadog-recommended-monitors/
[60]: /monitors/manage/
[61]: /monitors/create/
[62]: https://www.youtube.com/watch?v=Ma5pr-u9bjk
[63]: /monitors/guide/why-did-my-monitor-settings-change-not-take-effect/
[64]: /monitors/notify/downtimes/
[65]: https://www.datadoghq.com/blog/mute-datadog-alerts-planned-downtime/
[66]: https://www.datadoghq.com/blog/managing-datadog-with-terraform/
[67]: /api/latest/downtimes/
[68]: /monitors/guide/prevent-alerts-from-monitors-that-were-in-downtime/
[69]: /integrations/slack/?tab=slackapplication
[70]: /integrations/pagerduty/
[71]: /integrations/flowdock/
[72]: /integrations/servicenow/
[73]: /integrations/google_hangouts_chat/
[74]: /integrations/microsoft_teams/
[75]: /integrations/
[76]: /integrations/webhooks/
[77]: /monitors/notify/
[78]: https://www.datadoghq.com/blog/send-alerts-sms-customizable-webhooks-twilio/
[79]: https://www.datadoghq.com/blog/monitoring-101-collecting-data/
[80]: /dashboards/widgets/timeseries/
[81]: /dashboards/widgets/free_text/
[82]: https://learn.datadoghq.com/courses/building-better-dashboards
[83]: /notebooks/
[84]: https://www.datadoghq.com/blog/network-device-monitoring/
[85]: https://www.datadoghq.com/blog/template-variable-associated-values/
[86]: /api/latest/dashboards/
[87]: https://www.hashicorp.com/resources/configure-observability-as-code-with-terraform-and-datadog
[88]: /dashboards/sharing/
[89]: /api/latest/dashboards/
[90]: /api/latest/embeddable-graphs/
[91]: /dashboards/guide/embeddable-graphs-with-template-variables/
[92]: https://www.datadoghq.com/blog/establishing-service-level-objectives/
[93]: /monitors/guide/slo-checklist/
[94]: https://www.datadoghq.com/blog/define-and-manage-slos/
[95]: https://www.datadoghq.com/blog/slo-monitoring-tracking/
[96]: /api/latest/service-level-objectives/
[97]: /monitors/create/types/watchdog/
