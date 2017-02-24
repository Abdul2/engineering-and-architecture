## Twelve Factor App

The [Twelve Factor App](https://12factor.net/) is a methodology for building software as a service. The twelve factors are:

1. One app per code repository
    - all code should be stored a repository such as git, one app per repo
    - multiple repositories (e.g. web front end and backend API) = multiple apps = a distributed system
    - shared code should be put into libraries which are included via a dependency manager
    - a deploy is a running instance of an app
2. Dependency declaration
    - all dependencies are declared exactly via a dependency manifest
    - if the app needs to shell out to a system tool, that tool should be vendored into the app
3. Store config in the environment
    - config that varies between deploys (e.g. db handles, credentials, API keys, hostnames) should be stored in env vars and NEVER in code
    - all config should be stored in a separate place from the code and be read in by the code at runtime when you deploy code somewhere
4. Backing services are attached resources
    - your code will talk to many services e.g. a database, a cache, an email service, a queueing system. Such backing services require a network connection to run
    - they should be accessed via a URL held in config and communicate via an API; this facilitates loose coupling
    - local backing services (e.g. MySQL) should be able to be switched out with 3rd party ones (e.g. Amazon RDS) without changing code
5. Separate build, release and run stages
    - building converts code into executable bundle. Commit version + dependencies  -> compiled binaries + assets
    - a release sends that code to a server in a package with the separate deploy config files for that environment. It should have a unique releaseId and is immutable
    - running launches an app against the release; it should be a simple and robust procedure
6. Processes - execute the app as one or more stateless processes
    - processes are stateless (temporary storage for a single request is ok) and share nothing
    - if persistent storage is required, use a backing service
    - don’t use sticky sessions (session data cached in the app’s process memory), instead store in a datastore with time expiration e.g. [ElastiCache](https://aws.amazon.com/elasticache/)
7. Export services via port binding
    - apps should be accessible via a URL (be self contained) and NOT require a container (such as Websphere or Tomcat) to run
    - apps export HTTP as a service and bind to a port by using a webserver library added to the app (e.g [Netty](http://netty.io/))
8. Concurrency - scale out the process model
    - your running app should have many small, independent processes to perform different tasks
    - each process should be able to scale, restart, or clone itself independently when needed
9. Disposability — fast startup and graceful shutdown
    - processes should be quick to start
    - they should shutdown gracefully when they receive a SIGTERM; they should stop listening on port, finish off request then exit
    - your app should be robust against crashing. If it does crash it should be able to restart cleanly: all jobs should be reentrant (wrapped in a transaction or idempotent)
10. Dev / prod parity
    - tools: dev, staging, prod as similar as possible
    - time: don’t have long gaps between deploying to dev / preprod / prod
    - personnel: don’t have developers write code, ops engineers deploy it. Have the same personnel involved in these stages
11. Logs as event streams
    - the app should not concern itself with routing or storing its logging output
    - each running process writes its event stream, unbuffered, to stdout
    - logs are viewed by developers in their local consoles and in prod they are automatically captured as a stream of events and pushed into a consolidated system such as [Logstash](https://www.elastic.co/products/logstash)
12. Admin access via a REPL
    - console access to prod is a critical administrative and debugging tool
    - most languages have a [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop) which makes it easy to run scripts in the appropriate execution environment
    - one-off admin processes should ship with application code and run against a release, using the same codebase and config
  
