
# Engineering and Architecture principles

|   |    |   |   |
|---|---|---|---|
|1|Follow [Lean principles](#lean)|10|[Continuous delivery](#cd) over change management
|2|Follow [Domain Driven Design](#ddd)|11|Services designed around [user needs](#user-needs)
|3|Minimise [vendor lock-in](#vendor-lock-in)|12|Build for [modern web browsers](#modern-browser-first) and don't build mobile apps
|4|Services built as [twelve factor](#twelve-factor) apps|13|Information is an [asset with an owner](#iao)
|5|[Loosely coupled](#loosely-coupled) services over monoliths|14|Follow [our standards] (#follow-standards) for languages, frameworks, techniques and tools
|6|[Shared services](#shared-services) over shared code|15|[Commodity cloud](#commodity-cloud) first
|7|[Cooperative architecture](#cooperative-architecture) over siloed architecture|16|Use our [common platforms](#common-platforms)
|8|[Secure systems](#secure-systems) over secure zones|17|[Open](#open) standards, open data, open source
|9|Services and data appropriately [protected and accessed](#protected-services)|18|Build for [operational readiness](#operational-readiness)


## <a name="lean"></a>1 Lean Principles
1. [Eliminate Waste](http://www.allaboutagile.com/lean-principles-1-eliminate-waste/) (e.g. unecessary code or functionality, poor communication, incomplete work, context switching, defects)
2. [Build Quality In](http://www.allaboutagile.com/lean-principles-2-build-quality-in/) (by [pairing](http://www.jamesshore.com/Agile-Book/pair_programming.html), test driven development, constant feedback, frequent integration and automation)
3. [Create Knowledge](http://www.allaboutagile.com/lean-principles-3-create-knowledge/) (by [pairing](http://www.jamesshore.com/Agile-Book/pair_programming.html), code reviews, wikis, SIGs)
4. [Defer Commitment](http://www.allaboutagile.com/lean-principles-4-defer-commitment/) (especially when things are prone to change)
5. [Deliver Fast](http://www.allaboutagile.com/lean-principles-5-deliver-fast/) (by getting the right team and working as a team, keeping it simple)
6. [Respect People](http://www.allaboutagile.com/lean-principle-6-respect-people/)
7. [Optimise The Whole](http://www.allaboutagile.com/lean-principle-7-optimise-the-whole/)

## <a name="ddd"></a>2 Domain Driven Design
* Use a common, [ubiquitous language](http://www.jamesshore.com/Agile-Book/ubiquitous_language.html) across the business domain and architecture / code

## <a name="vendor-lock-in"></a>3 Avoid vendor lock-in
xxx

## <a name="twelve-factor"></a>4 Twelve-factor app
1. One app per repository
    - all code is in a repository such as git
    - multiple apps sharing the same code is a violation
    - multiple repositories = multiple apps = a distributed system
    - shared code should be put into libraries which are included via a dependency manager
    - a deploy is a running instance of an app
2. Dependency declaration
    - all dependencies are declared exactly via a dependency manifest
    - if the app needs to shell out to a system tool, that tool should be vendored into the app
3. Config in env vars
    - config that varies between deploys (e.g. db handles, credentials, API keys, hostnames) should be stored in env vars and NEVER in code
4. Backing services are attached resources
    - a backing service is one that requires a network connection to run e.g. database, message queue
    - they are loosely coupled to the app, accessed via a URL held in config and communicate via an API
    - local backing services (e.g. MySQL) should be able to be switched out with 3rd party ones (e.g. Amazon RDS) without changing code
5. Separate build, release and run stages
    - building converts code into executable bundle. Commit version + dependencies  -> compiled binaries + assets
    - a release combines executable bundle with deploy config and should have a unique releaseId. A release is immutable
    - running launches an app against the release; you cannot change code here
6. Stateless processes
    - processes are stateless (temporary storage for a single request is ok) and share nothing
    - if persistent storage is required, use a backing service
    - don’t use sticky sessions (session data cached in the app’s process memory), instead store in a datastore with time expiration e.g. Redis
7. Export services via port binding
    - apps should be accessible via a URL (be self contained) and NOT require a container (such as Websphere or Tomcat) to run
    - apps export HTTP as a service and bind to a port by using a webserver library added to the app (e.g Jetty for Java)
8. Process concurrency
    - processes are 1st class citizens which can be scaled independently
    - each process should be able to scale, restart, or clone itself when needed
9. Processes are disposable (easy to start and stop)
    - quick to start
    - shutdown gracefully when they receive a SIGTERM (they should stop listening on port, finish off request then exit). Locks are released and worker jobs go back onto a queue
    - all jobs are reentrant (wrapped in a transaction or idempotent)
10. Dev / prod parity
    - tools: dev, staging, prod as similar as possible
    - time: don’t have long gaps between deploying to dev / preprod / prod
    - personnel: don’t have developers write code, ops engineers deploy it. Have the same personnel involved in these stages
11. Logs as event streams
    - the app should not concern itself with routing or storing its logging output
    - each running process writes its event stream, unbuffered, to stdout
12. Admin in the codebase or REPL
    - One-off admin processes should ship with application code and be run in an identical environment as the regular long-running processes of the app. They run against a release, using the same codebase and config
    - favour languages with a REPL, which makes it easy to run scripts in the appropriate execution environment

## <a name="loosely-coupled"></a>5 Loose Coupling
xxx

## <a name="shared-services"></a>6 Shared Services
xxx

## <a name="cooperative-architecture"></a>7 Cooperative Architecture
xxx

## <a name="secure-systems"></a>8 Secure Systems
xxx

## <a name="appropriate-protection"></a>9 Appropriate Protection
xxx

## <a name="cd"></a>10 Continous Delivery
Build the expectation of regular updates (on a scale of minutes, not days or weeks) into your release process to ensure that changes are repeatable, reliable, and fast. Only by releasing often can you become good at releases, and make them low risk. By having long change processes to follow, the team (and service) become change-averse, and change becomes difficult and dangerous.

## <a name="user-needs"></a>11 User Needs
xxx

## <a name="modern-browser-first"></a>12 Modern Browser First
xxx

## <a name="iao"></a>13 Information Asset Owner
xxx

## <a name="follow-standards"></a>14 Follow our standards
xxx

## <a name="commodity-cloud"></a>15 Commodity Cloud
Public cloud, provided at scale by commercial technology companies has emerged as the lowest risk environment for our information systems to reside. 

## <a name="common-platforms"></a>16 Common Platforms
xxx

## <a name="open"></a>17 Open standards, data, source
xxx

## <a name="operational-readiness"></a>18 Operational Readiness
xxx












