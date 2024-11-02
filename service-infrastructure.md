---
layout: page
title: Service Infrastructure
---
[Service Infrastructure](https://cloud.google.com/service-infrastructure/docs/overview) is described as Google's "foundational platform for creating, managing, securing, and consuming APIs and services across organizations."

Capabilities provided by Service Infrastructure include:
* authentication and authorization
* rate limiting
* logging, monitoring, analytics, and auditing

Virtually all of Google's APIs are built on Service Infrastructure, and Service Infrastructure can also be used for non-Google "third party" APIs. These APIs might be implemented using Google Cloud, but that's not necessary. Service Infrastructure can be used anywhere within reach of a Google Cloud data center, and the Service Infrastructure APIs are simple enough that they can be reimplemented and run anywhere.

Service Infrastructure is built on five public Google APIs.

1. The [Service Management](/service-management) API manages descriptions of APIs and configurations that control their access.
2. The [Service Control](/service-control) API is used to check API requests from consumers and to monitor requests and responses.
3. The [API Keys](/api-keys) API generates and manages API keys that consumers use to call APIs.
4. The [Cloud Logging](/cloud-logging) API allows applications to read logs describing API traffic.
5. The [Cloud Monitoring](/cloud-monitoring) API allows applications to read metrics describing API traffic.

A sixth API, [Service Usage](/service-usage), is used to control access to Google APIs within Google Cloud projects, and is used to enable the other APIs listed above.

In 2016, Google released the [Cloud Endpoints](/cloud-endpoints) API management product, which uses Service Infrastructure to manage APIs on Google Cloud and external platforms.
