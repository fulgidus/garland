---
clipped: 2026-04-27
url: https://12factor.net/
author: Adam Wiggins
---

# The Twelve-Factor App

GitHub
Introduction
In the modern era, software is commonly delivered as a service: calledweb apps, orsoftware-as-a-service. The twelve-factor app is a methodology for building software-as-a-service apps that:
Usedeclarativeformats for setup automation, to minimize time and cost for new developers joining the project;
Have aclean contractwith the underlying operating system, offeringmaximum portabilitybetween execution environments;
Are suitable fordeploymenton moderncloud platforms, obviating the need for servers and systems administration;
Minimize divergencebetween development and production, enablingcontinuous deploymentfor maximum agility;
And canscale upwithout significant changes to tooling, architecture, or development practices.
The twelve-factor methodology can be applied to apps written in any programming language, and which use any combination of backing services (database, queue, memory cache, etc).
Background
The contributors to this document have been directly involved in the development and deployment of hundreds of apps, and indirectly witnessed the development, operation, and scaling of hundreds of thousands of apps via our work on theHerokuplatform.
This document synthesizes all of our experience and observations on a wide variety of software-as-a-service apps in the wild. It is a triangulation on ideal practices for app development, paying particular attention to the dynamics of the organic growth of an app over time, the dynamics of collaboration between developers working on the app’s codebase, andavoiding the cost of software erosion.
Our motivation is to raise awareness of some systemic problems we’ve seen in modern application development, to provide a shared vocabulary for discussing those problems, and to offer a set of broad conceptual solutions to those problems with accompanying terminology. The format is inspired by Martin Fowler’s booksPatterns of Enterprise Application ArchitectureandRefactoring.
Who should read this document?
Any developer building applications which run as a service. Ops engineers who deploy or manage such applications.
The Twelve Factors
I. Codebase
One codebase tracked in revision control, many deploys
II. Dependencies
Explicitly declare and isolate dependencies
III. Config
Store config in the environment
IV. Backing services
Treat backing services as attached resources
V. Build, release, run
Strictly separate build and run stages
VI. Processes
Execute the app as one or more stateless processes
VII. Port binding
Export services via port binding
VIII. Concurrency
Scale out via the process model
IX. Disposability
Maximize robustness with fast startup and graceful shutdown
X. Dev/prod parity
Keep development, staging, and production as similar as possible
XI. Logs
Treat logs as event streams
XII. Admin processes
Run admin/management tasks as one-off processes
Česky (cs)|Deutsch (de)|Ελληνικά (el)|English (en)|Español (es)|فارسی (fa)|Français (fr)|Italiano (it)|日本語 (ja)|한국어 (ko)|Polski (pl)|Português do Brasil (pt_br)|Русский (ru)|Slovensky (sk)|ภาษาไทย (th)|Türkçe (tr)|Українська (uk)|Tiếng Việt (vi)|简体中文 (zh_cn)
Written by Adam Wiggins • Last updated 2017 •Sourcecode•Download ePub Book
© Copyright 2026 Salesforce, Inc. All rights reserved. Various trademarks held by their respective owners. Salesforce Tower, 415 Mission Street, 3rd Floor, San Francisco, CA 94105, United States
LegalTerms of ServicePrivacy InformationResponsible DisclosureTrustContactYour Privacy ChoicesCookie Preferences
