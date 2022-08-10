---
title: Getting started for managed service providers
kind: documentation
description: "Best practices and guides for getting started with monitoring clients' environments."
---

Datadog provides insights into your clients' hybrid cloud infrastructures and applications. The intuitive UI and powerful API allows you to onboard, provision, and manage your clients' diverse environments, while establishing data security in each account.

This document covers some best practices and guides you through getting started with monitoring your clients' environments. The document is split into four main sections:

- [Laying the Groundwork](#laying-the-groundwork): Contains information about how to get started and which key decisions you should make at the very beginning.
- [Data Intake](#data-intake-getting-data-to-datadog): Explains how data can be fed into Datadog and which prerequisites need to be met in your or your clients' environments.
- [Delivering Value](#delivering-value): Walks through recommended steps once you have data flowing into Datadog.
- [Up & Running](#up--running): Covers how to stay up to date with the Datadog platform. Should you have any questions or feedback about any of these best practices, reach out to your Partner Account Manager.

## Key considerations for managed service providers (MSPs)

The way you as a service provider get started with Datadog depends on your business model and your operational model:

- **Business model**: A key question to answer is whether you are planning on giving your clients their own access to Datadog or not. If you do choose to give clients access to Datadog, set up a multi-organization account to keep client data separate and private.
- **Operational model**: Another key consideration is whether your client base consists of many homogeneous clients, where programmatic management of many similar-looking Datadog organizations is more important, or whether your clients are fewer or more heterogeneous.

## Laying the groundwork

### Prerequisites

Before working on implementing Datadog as a Service Provider, it is recommended that you complete the [Datadog Technical Specialist training][1] available exclusively for Datadog partners.

The training and certification familiarize you with many of the topics covered in the next chapters, enabling you to get started immediately.

### Organization setup

One of the key decisions for a Service Provider to make is how to set up client Datadog accounts, called "Organizations" (or "orgs" for short). While users can be associated with more than one organization, monitored resources are tied to a single organization. Choosing the right organization structure from the beginning helps to quickly create value for you and your clients.

#### Single-organization or multiple-organization

Datadog offers the possibility of managing multiple child organizations from one parent organization. This is the typical deployment model used by MSPs to prevent clients from having access to each others' data. In a multi-org setup, one child organization is created for each client, and the client is restricted to their own child organization. 

Use a single-org setup if you have no plans to give your clients access to Datadog and do not have a strict requirement to separate client data.

For more information about Organization Management, see the [Managing Multiple Organization Accounts][2] documentation.

#### Separate orgs for dev, test and production?

A common question from MSP partners is whether separate Datadog orgs should be set up to manage development, test, and production resources in environments.

Datadog does not recommend separating development, test, and production resources. The recommended approach is to manage all resources in the same Datadog organization and delineate the environments through tags. For more information, see [Tagging strategy](#tagging-strategy).

### Custom subdomains

To improve your Datadog experience when handling a large number of organizations, use the custom subdomain feature.

By default, any Datadog organization is accessed through Datadog's access pages, [https://app.datadoghq.com][3] and [https://app.datadoghq.eu][4]. However, custom subdomains can provide a unique URL for each sub-organization. For example, `https://account-a.datadoghq.com`. 

For more information, see [Custom sub-domains][5]).

### User roles and custom role-based access control (RBAC)

Experience shows that both MSP-internal and client users often do not fall clearly into one of the three [Datadog default roles][6]. It's good practice to create custom roles to limit user permissions in certain areas. 

For more information, see:
- [Custom roles][7]
- [Role Based Access Control][8]

### Single sign-on (SSO) considerations

In a service provider context, you have two considerations for Single sign-on (SSO):
- Single sign-on for your organization
- Single sign-on for your clients

Besides the obvious advantage of a unified authentication mechanism, using SAML Single Sign-On also vastly simplifies the user provisioning process. Using SAML allows you to use Just-in-Time (JiT) user provisioning, eliminating the need to manually or programmatically create users.

SAML authentication is enabled on a Datadog organization or sub-org, meaning you can have different SAML providers for different sub-orgs. However, this also means that if you have two groups of users with different SAML providers, those users have to be in separate orgs. Make sure you think about SAML authentication when when planning your multi-organization setup.

For more information, see:
- [Set up SAML][9] for multiple-organization accounts
- [Single sign-on with SAML][10]

### Managing users

#### User creation

Datadog offers multiple ways to quickly provision users for their respective organizations:

- [Add batches of users through the UI][11] 
- [Create users through the API][12]
- Use an authentication service like SAML together with [Just-in-Time (JiT) provisioning][13]

#### User training

Datadog's goal is to provide a service that is easy and intuitive to use. Experience shows that most users feel comfortable working with the product, and learning as they go along.

Here are some useful resources for users that prefer to have training on the most important aspects of the product:

- [Datadog's YouTube channel][14]: With introduction videos posted whenever new features are released as well as videos on Tips & Tricks and Best Practices, Datadog's YouTube channel is a great source for high-level training.
- [Datadog Learning Center][15]: The Datadog Learning Center is a great way for users to get to know the platform in-depth. When signing up for the Learning Center, a Datadog sandbox environment is automatically provisioned free of charge, allowing users to play around with the product without fear of breaking anything.
- [The Datadog Blog][16]: With over 700 entries, The blog is a key source of information on how to use Datadog to monitor key services, tools, and technologies in your client environments, as well as information on the latest product releases.
- [Datadog Partner Network (DPN) Enablement Center][17]: Through the DPN, Datadog service provider partners have access to a series of video courses for service provider salespeople and technical professionals.

Reach out to your Datadog partner representative if you plan on building your own training material for your clients and have any recommendations on what content would be helpful.

## Data intake

It's time to start getting data into Datadog. Datadog offers several different ways to collect data:
- Cloud service integrations (out of the box)
- The Datadog Agent & Agent-based Integrations (out of the box)
- APIs / Library Integrations & Custom Checks

Initially, the objective of this phase should be to gather data to provide immediate value to you or your clients. However, in the long run, you should consider this an ongoing process where you constantly assess changes to your environment by asking the following questions:
- Have you or your clients employed a new technology?
- Have you or your clients introduced a new process?
- Has Datadog introduced a new product feature that you can use? 
 
Consider these questions regularly to ensure that all necessary telemetry is being ingested into Datadog.

### Integrations

You can provide immediate value to your clients through integrations. Datadog offers {{< translate key="integration_count" >}} integrations, which collect metrics and logs from a wide array of technologies. Some integrations come packaged with the Datadog Agent, others are authentication-based and rely on the Datadog API, and some collect data based on the language that an application is written in.

For more information on integrations and the Datadog Agent, see:
- [Introduction to Integrations][18]
- [List of Datadog Integrations][19]
- [The Datadog Agent][20]
- [Getting Started with the Agent][21]

### APIs / library integrations and custom checks

Datadog focuses on scalability and extensibility, and offers several APIs and SDKs to extend the platform in situations where:
- Installing the Agent might not be possible due to security or other restrictions, for example on IoT devices.
- The capabilities of the Datadog Agent and its integrations do not cover a technology or requirement.

In these cases, using APIs enables you to capture relevant telemetry into the observability platform for your clients.

There are three key API areas that would be of most interest to you as a service provider:
- Public APIs for data ingestion
- Custom checks
- Local APIs for data ingestion on the Agent

#### Public APIs for data ingestion

In cases where using cloud service integrations or the Agent is not possible or desired, the following APIs can be helpful for data intake:

- Logs can be forwarded directly to Datadog's [log ingestion endpoint][22].
- Metrics can be forwarded directly to Datadog's [metrics API][23].
- Events can be forwarded directly to Datadog's [events API][24].
- Traces can be forwarded directly to Datadog's [trace/span API][25].

#### Custom checks

While Datadog offers {{< translate key="integration_count" >}} integrations, your client might run a custom application that cannot be covered with any of the existing integrations. To monitor these applications, your clients can use the Agent to execute custom checks.

For more information, see [Custom Checks][26].

#### Local APIs for data ingestion on the Agent

The Datadog Agent comes bundled with DogStatsD, a metrics aggregation service, which accepts data using UDP. DogStatsD is a good alternative if a custom check does not suit your use case and there are no existing integrations for the application. For example, you can use DogStatsD to collect events and metrics data from a cron job, which probably does not have its own log files.

You can either use the DogStatsD endpoints, or use a Datadog client library to facilitate the submission of metrics and events to DogStatsD.

For more information, see:
- [Submit Events][27]
- [Submit Custom Metrics][28]
- [Libraries][29]
- [API Reference][30]

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

- [Getting Started with Tags][31]
- [Best practices for tagging your infrastructure and applications][32] (Blog)
- [Tagging Best Practices][33] (Training)

Tagging strategy: 
- [Unified Service Tagging][34]
- [Kubernetes Tag Extraction][35]
- [AWS Tagging][36] (AWS Documentation)
- [Serverless Tagging][37]
- [Live Container Tagging][38]

### Agent rollout

As we've seen in the previous sections, there are many benefits to using the Datadog Agent for data collection. Below we'll cover four phases of Agent rollout:

- Prerequisites for Agent deployment
- Initial Agent deployment to the existing infrastructure
- Provisioning of new infrastructure
- Monitoring the continuous provisioning processes

#### Prerequisites for Agent deployment

Depending on the platform and operating system, there might be different prerequisites for the Agent. See [the official Agent documentation][39] to familiarize yourself with those requirements.

The main prerequisite for the Agent on any platform is network connectivity. Traffic is always initiated by the Agent to Datadog. No sessions are ever initiated from Datadog back to the Agent. Except in rare cases, inbound connectivity (limited through local firewalls) is not a factor for Agent deployments.

To work properly, the Agent requires the ability to send traffic to the Datadog service over SSL via 443/tcp. For a full list of ports ports used by the agent, see [Network Traffic][40].

In some circumstances, Agent version-specific endpoints can cause maintenance problems, in which case we can provide a version-agnostic endpoint. If you need a version-agnostic endpoint, contact Datadog support.

##### Agent proxy

In many client environments, opening direct connectivity from the Agent to Datadog is not possible or desired. To enable connectivity, Datadog offers a few different options to proxy the Agent traffic.

For more information, see [Agent Proxy Configuration][41].

#### Agent deployment, upgrade, and configuration

There are various ways to deploy the Datadog Agent to your own and your client's infrastructure. As most service providers already have some configuration management tool in place, it is good practice to use the existing tool for Agent rollout.

Here are some examples of how to manage your Datadog Agent estate with configuration management tools:
- [Deploying Datadog Agents with Chef][42] (Blog)
- [Puppet + Datadog: Automate + monitor your systems][39] (Blog)
- [Deploying and Configuring Datadog with CloudFormation][43] (Blog)
- [How to Use Ansible to Automate Datadog Configuration][44] (Video)
- [How to deploy the Datadog agent on AWS hosts with Ansible dynamic inventories][45] (Blog)

If you don't plan on using Datadog's repositories, you can always find the latest Agent releases in the [public Github repository][46]. It is recommended that you [verify the distribution channel][47] of Agent packages before deployment.

#### Monitoring the continuous provisioning processes

While it is good practice to not only use configuration management tools for deploying Datadog, we also recommend leveraging Datadog to monitor proper operation of the tools. Here are some examples:

- [Ask your systems what's going on: monitor Chef with Datadog][48] (Blog)
- [Ansible + Datadog: Monitor your automation, automate your monitoring][49] (Blog)

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
- [Monitoring 101 - Alerting on what matters][50] (blog).
- [Intro to Monitoring][51] (Training).

#### Thoughts about monitor migrations

A frequent situation service providers can find themselves in is migrating a client from a different monitoring or observability platform to Datadog. In such cases, it might seem logical to simply replicate any monitor from the previous solution to Datadog. However, experience shows that with this approach many of Datadog's features that improve issue detection and resolution times or reduce alert fatigue will remain unused.

We therefore recommend that as part of such a migration project, existing alert/threshold definitions should be reviewed to answer if:

- The metric has a time-based variation, in which case [an Anomaly Monitor][52] might be a better approach.
- The metric has a load-based variation, in which case an [arithmetic monitor][53] might be the best approach by combining a metric with a load- indicating metric (i.e., load on the systems might be higher if there are more users using a service).
- The absolute value of the metric is less important than the rate of change, in which case a [change monitor][54] or a [forecast monitor][55] might be the best approach.
- The value of the metric itself is less important than whether it is different from the value for other hosts or entities (i.e., one node in a cluster is experiencing high latency where other nodes are not), in which case the [outlier monitor][56] is the best approach.
- Only the combination of multiple metrics present an actionable situation, in which case [composite monitors][57] offer an easy way without any scripting needed.

#### Programmatic monitor management

As a service provider, management of possibly very large amounts of monitors for you and your clients is best accomplished programmatically through one of the following ways:

- [Datadog Monitors API][58]
- Terraform
  - [How to Manage Datadog Resources Using Terraform][59] (Video)
  - [Automate Monitoring with the Terraform Datadog Provider][60] (HashiCorp Tutorial)

We also recommend that you [tag monitors][61] to make the management of large numbers of monitors easier.

#### Recommended monitors

While creating monitors for technologies that you manage on a daily basis might be straightforward, chances are that you will run into technologies your clients operate that you as the service provider might not have a lot of experience with. It's for situations like these that Datadog offers [Recommended Monitors][62] to help you onboard new technologies quickly and confidently.

To find out more about Monitors, see:
- [Manage Monitors][63]
- [Monitors][64]
- [Creating Dynamic Alerts Using Tag Values][65] (Video)
- [Why Did My Monitor Settings Change Not Take Effect?][66] (FAQ)

#### Downtimes

A common problem with monitors and alerts is alert fatigue, where an overabundance of alarms or notifications causes desensitization to the alarms. One way to combat alert fatigue is to limit the number of false positive alarms, especially in controlled situations such as planned system shutdowns, maintenance, or upgrade-windows.

Datadog's Downtimes offer you and your clients a way to mute monitors during times of planned (or ad hoc) maintenance.

To find out more about managing downtimes, especially programmatically, see:
- [Downtime][67]
- [Mute Datadog Alerts for Planned Downtimes][68] (Blog)
- [Managing Datadog with Terraform][69] (Blog)
- [Downtime API][70]
- [Prevent alerts from Monitors that were in downtime][71]

#### Notifications

Some general guidelines for notifications:
- Alert liberally; page judiciously
- Page on symptoms, rather than causes

Datadog offers various channels through which you or your clients can notify users about important alerts:

- Email notifications
- Integrations, such as:
  - [Slack][72]
  - [PagerDuty][73]
  - [Flowdock][74]
  - [ServiceNow][75]
  - [Google Hangouts Chat][76]
  - [Microsoft Teams][77]
  - And [many more][19]

You can also invoke any REST API using the generic [Webhooks integration][78], which can be used not only to notify users but also to trigger automatic remediation workflows.

To find out more about Notifications, see:

- [Notifications][79]
- [Send SMS Alerts with Webhooks and Twilio][80] (Blog)

### Setting up visualizations with Dashboards 

Visualizations are a great way to give your clients a clear picture of complex tech stacks and abundance of metrics and events being collected. Dashboards are a natural starting point to investigate a potential issue you or your client was notified about by a monitor.

#### Out-of-the-box dashboards

The moment that an Agent or Cloud Integration is set up, Datadog automatically enables out-of-the-box dashboards for the newly integrated service or technology, providing immediate insights. Out-of-the-box dashboards can also be cloned, giving you a great starting point for a custom dashboard.

#### Building custom dashboards

By not only offering a technology-centric perspective to your clients but also a business-centric perspective, tailored to different personas, you as a service provider can provide extra value and distinguish yourself from your competitors.

There are a number of dashboard best practices we recommend you take into consideration when building your dashboards:

- Focus on work metrics rather than too many resource metrics. To understand the difference, see [Monitoring 101: Collecting the right data][81] (blog).
- Make use of [event overlays][82] to correlate metrics and events.
- Annotate the dashboards with [free text information][83] on what data is shown and what to do in case the dashboard indicates an issue.

To find out more about Dashboards, see:
- [Building Better Dashboards][84] (Training)
- Use the [Datadog Notebooks][85] feature to gather data in an exploratory fashion and draft dashboards
- [Monitor Datacenters and Networks with Datadog][86] (Blog)
- [Use Associated Template Variables][87] (Blog)
- [The Datadog Dashboard API][88]
- [Configure Observability as Code with Terraform & Datadog][89] (HashiCorp webinar)

#### Visualizations for users without Datadog access

Depending on your business model, your clients might not require access to Datadog themselves but you might still want to provide Datadog visualizations to your clients. To do this, you have the following options:
- [Dashboard sharing][90]: Share a read-only dashboard via public URL to provide a status page to your clients or share it privately using an individual e-mail address.
  - As a service provider, your business needs to be able to scale. Therefore [managing shared dashboards via our APIs][88] will probably be the most efficient approach.
- Embeddable graphs: If you have a client portal in which you want to present Datadog information, Embeddable Graphs are the way to go. By using parameters, you can filter data according to your needs. 
  For more information, see:
  - [Embeddable Graphs API][91]
  - [Embeddable Graphs with Template Variables][92]


#### Setting up Service Level Objectives (SLOs)

As a service provider it is a good idea to continually present the quality and level of your services to your clients in a transparent way. Service Level Objectives (SLOs) are a great way to monitor and visualize the service quality on behalf of your clients, and also help your clients implement service level-based reporting internally.

The following material might be helpful for you when setting up and managing SLOs:
- To get started, we recommend [Service Level Objectives 101: Establishing Effective SLOs][93] (Blog). 
- [SLO Checklist][94]
- [Best practices for managing your SLOs with Datadog][95] (Blog)
- [Track the status of all your SLOs in Datadog][96] (Blog)
- [The Datadog SLO API][97]

### Using Watchdog

Watchdog is an algorithmic feature that automatically detects potential application and infrastructure issues.

We recommend that you set up a Watchdog Monitor for your own staff or your client with a notification whenever Watchdog has detected a new irregularity.

For more information, see [Watchdog][98]

## Up & Running

In this chapter, we cover how to monitor both individual client and aggregate usage of the Datadog platform, and stay up to date with Datadog.

### Billing & Usage Reporting

Note: The details in this section apply to a Multi-Organization account setup

With a Datadog [admin role][8] in the parent organization you can view the total and billable usage of all your organizations (both child and parent) as well as how your clients' usage has changed over the past six months [as explained here][2].

Usage is aggregated across all child organizations and billed at the parent organization level. From the parent organization, those with an admin role can view aggregate usage across all child organizations as well as drill into usage of individual child organizations.

In case existing roles are not flexible enough for you or your client organization, you can create new custom roles. With custom roles, in addition to the general permissions, it is possible to define more granular permissions for specific assets or data types. You can find the list of permissions specific to [billing and usage assets here][99].

In addition to the usage page, below you will find a number of additional resources which might help you as a service provider estimate and manage clients' usage as well as provide easy allocations and chargebacks:

- [Estimated Usage Metrics][100]: Datadog calculates your clients' current estimated usage in near real-time. Estimated usage metrics enable you to graph your estimated usage, create monitors or alerts around your estimated usage based on thresholds of your choosing and get instant alerts on spikes or drops in your usage.

- [Shared Dashboards][90]: Shared dashboards and graphs allow you to display metric, trace, and log visualizations with your users outside of Datadog. You can publish estimated usage metrics dashboards for your clients to track.

- [Usage Attribution][101]: The Usage Attribution page provides: lists to the existing tag keys that usage is being broken down by and provides the ability to change and add new ones; generates daily .tsv (tab separated values) files for most usage types; and summarizes usage at the end of each month not only by child-organizations but also by tag. Please note that usage attribution is an advanced feature included in the Enterprise plan. For all other plans, contact your Datadog partner representative to request this feature.

[1]: https://partners.datadoghq.com/prm/English/c/technical_content
[2]: /account_management/multi_organization/
[3]: https://app.datadoghq.com
[4]: https://app.datadoghq.eu
[5]: /account_management/multi_organization/#custom-sub-domains
[6]: /account_management/rbac/?tab=datadogapplication#datadog-default-roles
[7]: /account_management/rbac/?tab=datadogapplication#custom-roles
[8]: /account_management/rbac/
[9]: /account_management/multi_organization/#set-up-saml
[10]: /account_management/saml/
[11]: /account_management/users/#add-new-members-and-manage-invites
[12]: /api/latest/users/#create-a-user
[13]: /account_management/saml/#just-in-time-jit-provisioning
[14]: https://www.youtube.com/user/DatadogHQ
[15]: https://learn.datadoghq.com/
[16]: https://www.datadoghq.com/blog/
[17]: https://partners.datadoghq.com/
[18]: /getting_started/integrations/
[19]: /integrations/
[20]: /agent/
[21]: /getting_started/agent/
[22]: /getting_started/logs
[23]: /api/latest/metrics
[24]: /api/latest/events
[25]: /api/latest/tracing/
[26]: /developers/custom_checks/
[27]: /events/guides/dogstatsd/
[28]: /metrics/custom_metrics/
[29]: /developers/community/libraries/#api-and-dogstatsd-client-libraries
[30]: /api/latest/
[31]: /getting_started/tagging/
[32]: https://www.datadoghq.com/blog/tagging-best-practices/
[33]: https://learn.datadoghq.com/courses/tagging-best-practices
[34]: /getting_started/tagging/unified_service_tagging?tab=kubernetes
[35]: /agent/kubernetes/tag/
[36]: https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html
[37]: /serverless/serverless_tagging/?tab=serverlessframework#overview
[38]: /infrastructure/livecontainers
[39]: /agent/basic_agent_usage/
[40]: /agent/guide/network/
[41]: /agent/proxy/
[42]: https://www.datadoghq.com/blog/deploying-datadog-with-chef-roles/
[43]: https://www.datadoghq.com/blog/monitor-puppet-datadog/
[44]: https://www.datadoghq.com/blog/deploying-datadog-with-cloudformation/
[45]: https://www.youtube.com/watch?v=EYoqwiXFrlQ
[46]: https://github.com/DataDog/datadog-agent/releases
[47]: /data_security/agent/#agent-distribution
[48]: https://www.datadoghq.com/blog/monitor-chef-with-datadog/
[49]: https://www.datadoghq.com/blog/ansible-datadog-monitor-your-automation-automate-your-monitoring/
[50]: https://www.datadoghq.com/blog/monitoring-101-alerting/
[51]: https://learn.datadoghq.com/courses/intro-to-monitoring
[52]: /monitors/create/types/anomaly/
[53]: /monitors/guide/monitor-arithmetic-and-sparse-metrics/
[54]: /monitors/create/types/metric/?tab=change
[55]: /monitors/create/types/forecasts/?tab=linear
[56]: /monitors/create/types/outlier/?tab=dbscan
[57]: /monitors/create/types/composite/
[58]: /api/latest/monitors/
[59]: https://www.youtube.com/watch?v=Ell_kU4gEGI
[60]: https://learn.hashicorp.com/tutorials/terraform/datadog-provider
[61]: https://www.datadoghq.com/blog/tagging-best-practices-monitors/
[62]: https://www.datadoghq.com/blog/datadog-recommended-monitors/
[63]: /monitors/manage/
[64]: /monitors/create/
[65]: https://www.youtube.com/watch?v=Ma5pr-u9bjk
[66]: /monitors/guide/why-did-my-monitor-settings-change-not-take-effect/
[67]: /monitors/notify/downtimes/
[68]: https://www.datadoghq.com/blog/mute-datadog-alerts-planned-downtime/
[69]: https://www.datadoghq.com/blog/managing-datadog-with-terraform/
[70]: /api/latest/downtimes/
[71]: /monitors/guide/prevent-alerts-from-monitors-that-were-in-downtime/
[72]: /integrations/slack/?tab=slackapplication
[73]: /integrations/pagerduty/
[74]: /integrations/flowdock/
[75]: /integrations/servicenow/
[76]: /integrations/google_hangouts_chat/
[77]: /integrations/microsoft_teams/
[78]: /integrations/webhooks/
[79]: /monitors/notify/
[80]: https://www.datadoghq.com/blog/send-alerts-sms-customizable-webhooks-twilio/
[81]: https://www.datadoghq.com/blog/monitoring-101-collecting-data/
[82]: /dashboards/widgets/timeseries/
[83]: /dashboards/widgets/free_text/
[84]: https://learn.datadoghq.com/courses/building-better-dashboards
[85]: /notebooks/
[86]: https://www.datadoghq.com/blog/network-device-monitoring/
[87]: https://www.datadoghq.com/blog/template-variable-associated-values/
[88]: /api/latest/dashboards/
[89]: https://www.hashicorp.com/resources/configure-observability-as-code-with-terraform-and-datadog
[90]: /dashboards/sharing/
[91]: /api/latest/embeddable-graphs/
[92]: /dashboards/guide/embeddable-graphs-with-template-variables/
[93]: https://www.datadoghq.com/blog/establishing-service-level-objectives/
[94]: /monitors/guide/slo-checklist/
[95]: https://www.datadoghq.com/blog/define-and-manage-slos/
[96]: https://www.datadoghq.com/blog/slo-monitoring-tracking/
[97]: /api/latest/service-level-objectives/
[98]: /monitors/create/types/watchdog/
[99]: /account_management/rbac/permissions/?tab=ui#billing-and-usage
[100]: /account_management/billing/usage_metrics/
[101]: /account_management/billing/usage_attribution/
